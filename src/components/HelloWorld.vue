<template>
  <div class="container">

    <div class="entry-header table-row">
      <div class="url-div">url</div>
      <div class="url-div">reciptient</div>
    </div>

    <div class="table-row" v-for="entry in email_entrys" v-bind:key="entry">
      <div class="url-div">{{entry.url}}</div>
      <div class="recipient">{{entry.to}}</div>
      <div class="subject">{{entry.subject}}</div>
      <div class="read">{{entry.read}}</div>
    </div>

    <br/>

    <form v-if="is_email_creator_open" v-on:submit.prevent="new_email">
      <input v-model="next_email.url">
      <input v-model="next_email.to" placeholder="recipient">
      <button type="submit">send to database</button>
      <button v-on:click="close_creator">dismiss</button>
    </form>

    <button class="add-button" v-else v-on:click="is_email_creator_open = true">+</button>

  </div>
</template>

<script>
export default {
  name: "Email Read Receipts",
  title: 'Emails',
  data: function() {
    return {
      email_entrys: [],
      next_email: {url: "https://"},
      is_email_creator_open: false,
    }
  },
  methods: {
    new_email: function() {
      this.email_entrys = [...this.email_entrys, this.next_email]
      localStorage.setItem('email_entrys', JSON.stringify(this.email_entrys))
      navigator.clipboard.writeText(this.next_email.url)
      this.is_email_creator_open = false

      // reset next email
      this.next_email = {url: "https://"}
    },
    close_creator: function() {
      this.is_email_creator_open = false
    }
  },
  mounted: function() {
    const existing_emails = localStorage.getItem('email_entrys')
    this.email_entrys = JSON.parse(existing_emails) || []
  }
}
</script>

<style scoped>

.entry-header{
  text-transform: uppercase;
  font-weight: bold;
  color: #888;
  font-size: 10px;
  padding-top: 2px;
  padding-bottom: 2px;
}
/* grow, truncate and show ellipsis when there is not enough space */
.url-div, .recipient {
  flex-grow: 1;            -webkit-flex-grow: 1;
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
  padding-right: 20px;
}

.url-div { width: 50px; }

.recipient { width: 50px; }

.table-row{
  display: flex;           display: -webkit-flex;
  flex-direction: row;     -webkit-flex-direction: row;
  flex-grow: 0;            -webkit-flex-grow: 0;
  flex-wrap: wrap;         -webkit-flex-wrap: wrap;
  width: 100%;
  padding-left: 15px;
  padding-right: 15px;
}

.container{
  display: flex;           display: -webkit-flex;
  flex-direction: column;     -webkit-flex-direction: column;
  flex-grow: 0;            -webkit-flex-grow: 0;
  flex-wrap: wrap;         -webkit-flex-wrap: wrap;
  justify-items: center;
  align-items: center;
  width: 100%;
  margin-top: 10px;
  margin-left: 15px;
  margin-right: 15px;
}

.add-button{
  width: 30px;
  height: 30px;
  border-radius: 10px;
  font-size: 20px;
  color: #888;
  border: 3px solid #888;
  background-color: #fff;
}

.add-button:hover{
  /* hiehgt width blur color */
  box-shadow: 0px 0px 5px 1px #ccc;
  color: #fff;
  background-color: #888;
}
</style>

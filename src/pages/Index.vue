<template>
  <div class="container-fluid">
  <h1>test</h1>
  <div class="row">
    <div class="col-md-12 buttons">
      <button type="button" name="button" @click="putOnDb" class="btn btn-primary">Put</button>
      <button type="button" name="button" @click="show" class="btn btn-primary">Show</button>
    </div>
  </div>

  <div class="row">
    <div class="col-md-8 db">
      <h2>Messages</h2>
      <table class="table table-bordered table-dark">
      <thead>
        <tr>
          <th>HE</th>
          <th>EN</th>
          <th>SP</th>
        </tr>
      </thead>
      <tbody v-for="item in data">
        <tr>
          <td></td>
          <td>$100</td>
        </tr>
      </tbody>
    </table>
    </div>
  </div>


  </div>
</template>

<script>
import Pouch from 'pouchdb-browser';

const db = new Pouch('database');
export default {
  name: 'app',

  created() {
    console.log(db);
  },

  data() {
    return {
      data: '',
    };
  },

  methods: {

    putOnDb() {
      const messages = { data: [
        {
          recordID: 1,
          Language: 'he',
          msgid: '1',
          msg: 'lo',
        },
        {
          recordID: 2,
          Language: 'he',
          msgid: '2',
          msg: 'mevin',
        },
        {
          recordID: 3,
          Language: 'he',
          msgid: '3',
          msg: 'klum',
        },
        {
          recordID: 4,
          Language: 'en',
          msgid: '1',
          msg: 'dont',
        },
        {
          recordID: 5,
          Language: 'en',
          msgid: '2',
          msg: 'undersant',
        },
        {
          recordID: 6,
          Language: 'en',
          msgid: '3',
          msg: 'anything',
        },
        {
          recordID: 7,
          Language: 'sp',
          msgid: '1',
          msg: 'no',
        },
        {
          recordID: 8,
          Language: 'sp',
          msgid: '2',
          msg: 'entende',
        },
        {
          recordID: 9,
          Language: 'sp',
          msgid: '3',
          msg: 'nada',
        },
      ] };
      // const locations = [
      //   {
      //     recordID: 1,
      //     Language: 'he',
      //     msgid: '1',
      //     msg: 'sherutim',
      //   },
      //   {
      //     recordID: 2,
      //     Language: 'he',
      //     msgid: '2',
      //     msg: 'kaspomat',
      //   },
      //   {
      //     recordID: 3,
      //     Language: 'he',
      //     msgid: '3',
      //     msg: 'supermarket',
      //   },
      //   {
      //     recordID: 4,
      //     Language: 'en',
      //     msgid: '1',
      //     msg: 'toilets',
      //   },
      //   {
      //     recordID: 5,
      //     Language: 'en',
      //     msgid: '2',
      //     msg: 'ATM',
      //   },
      //   {
      //     recordID: 6,
      //     Language: 'en',
      //     msgid: '3',
      //     msg: 'supermarket',
      //   },
      //   {
      //     recordID: 7,
      //     Language: 'sp',
      //     msgid: '1',
      //     msg: 'excusado',
      //   },
      //   {
      //     recordID: 8,
      //     Language: 'sp',
      //     msgid: '2',
      //     msg: 'Bank',
      //   },
      //   {
      //     recordID: 9,
      //     Language: 'sp',
      //     msgid: '3',
      //     msg: 'supermarket',
      //   },
      // ];
      db.post(messages, (err, result) => {
        console.log(err);
        console.log(result);
      });
      this.show();
    },

    show() {
      db.allDocs({ include_docs: true, descending: true }, (err, doc) => {
        this.data = doc.rows;
      });
    },

    remove(item) {
      console.log(item);
      db.remove(item);
    },

  },
};
</script>

<style>
.buttons {
  margin-bottom: 10px;
}
</style>

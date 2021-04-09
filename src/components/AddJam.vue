<template>
  <form @submit="onSubmit" class="add-form">
    <div class="form-control">
      <label>Add Jam Name</label>
      <input type="text" v-model="text" name="text" placeholder="Name" />
    </div>
    <div class="form-control">
      <label>Add Amount</label>
      <input
        type="text"
        v-model="amount"
        name="amount"
        placeholder="Amount"
      />
    </div>

    <input type="submit" value="Save Jam" class="btn btn-block" />
  </form>
</template>

<script>
export default {
  name: 'AddJam',
  data() {
    return {
      text: '',
      amount: ''
      //reminder: false,
    }
  },
  methods: {
    onSubmit(e) {
      e.preventDefault();

      if (!this.text) {
        alert('Please add a jam');
        return
      }

      const newJam = {
        // id: Math.floor(Math.random() * 100000),
        text: this.text,
        amount: this.amount
        //reminder: this.reminder,
      };

      this.$emit('add-jam', newJam);

      this.text = '';
      this.amount = ''
      //this.reminder = false
    },
  },
}
</script>

<style scoped>
.add-form {
  margin-bottom: 40px;
}

.form-control {
  margin: 20px 0;
}

.form-control label {
  display: block;
}

.form-control input {
  width: 100%;
  height: 40px;
  margin: 5px;
  padding: 3px 7px;
  font-size: 17px;
}

.form-control-check {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.form-control-check label {
  flex: 1;
}

.form-control-check input {
  flex: 2;
  height: 20px;
}
</style>

<template>
  <div class="editor">
    <textarea v-model="program" rows="30" cols="80" placeholder="Enter python code here"></textarea>
    <br>
    <button v-on:click=runProgram()>Run</button>
  </div>
  <div class="output">
    <hr>
    Output:<br>
    {{output["data"]["output"]}}
    <hr>
    Exit Code:<br>
    {{output["data"]["exitcode"]}}
    <hr>
    Error:<br>
    {{output["data"]["error"]}}
  </div>
</template>


<script>
import axios from "axios";
export default {
  name: 'Editor',
  data: () => ({
    output: {"data": {"output": "Click on run program", "exitcode": 0, "error": "None"}},
    program: null
  }),
  methods: {
    runProgram() {
      var config = {
        headers: {
            // 'Content-Length': 0,
            'Content-Type': 'text/plain'
        },
        responseType: 'json'
      };
      axios.post("https:ide.paramchauhan.com/python/execute", this.program, config).then((result) => {this.output = result})
    }
  }

};
</script>


<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>

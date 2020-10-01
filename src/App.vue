<!--
Copyright 2020 SpinalCom - www.spinalcom.com

This file is part of SpinalCore.

Please read all of the following terms and conditions
of the Free Software license Agreement ("Agreement")
carefully.

This Agreement is a legally binding contract between
the Licensee (as defined below) and SpinalCom that
sets forth the terms and conditions that govern your
use of the Program. By installing and/or using the
Program, you agree to abide by all the terms and
conditions stated or referenced herein.

If you do not agree to abide by these terms and
conditions, do not demonstrate your acceptance and do
not install or use the Program.
You should have received a copy of the license along
with this file. If not, see
<http://resources.spinalcom.com/licenses.pdf>.
-->

<template>
  <div class="main">
    <div>
      <textarea v-model="m_input"
                name=""></textarea>
    </div>
    <div>
      <pre>{{ out }}</pre>
    </div>
  </div>
</template>

<script>
const toJsonSchema = require("to-json-schema");
var YAML = require("json2yaml");
var toOpenApi = require("json-schema-to-openapi-schema");

export default {
  data() {
    return {
      m_input: "{}",
      out: ""
    };
  },
  watch: {
    m_input() {
      console.log("this.m_input",this.m_input);
      const schema = toJsonSchema(JSON.parse(this.m_input));
      console.log("schema",schema);

      const json = toOpenApi(schema);
      console.log("json",json);

      this.out = YAML.stringify(json);
      console.log(json);
    }
  }
};
</script>

<style>
#app,
.main {
  height: 100vh;
  width: 100vw;
  display: flex;
  position: relative;
}
.main > div,
.main > div > textarea {
  height: 95%;
  width: 95%;
  position: relative;
}
</style>

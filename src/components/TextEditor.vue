
<template>
  <div class="example">
    <div class="file-buttons">
      File: <input type="text" v-model="savingFileName" placeholder="Enter filename"/>
      <button @click="download()">Save</button>
      <input type="file" ref="doc" @change="readFile()" />
    </div>

    <quill-editor class="editor" ref="myTextEditor" :value="content" :options="editorOption" @change="onEditorChange"
      @blur="onEditorBlur($event)" @focus="onEditorFocus($event)" @ready="onEditorReady($event)" />
    <div>
  <ProjectFooter/>
</div>
  </div>
</template>

<script>
import dedent from 'dedent'
import hljs from 'highlight.js'
import debounce from 'lodash/debounce'
import { quillEditor } from 'vue-quill-editor'
import ProjectFooter from "./ProjectFooter.vue"

// highlight.js style
import 'highlight.js/styles/tomorrow-night-bright.css'

// import theme style
import 'quill/dist/quill.core.css'
import 'quill/dist/quill.snow.css'

export default {
  name: 'TextEditor',
  title: 'Theme: snow',
  components: {
    quillEditor,
    ProjectFooter
  },
  data() {
    return {
      file: null,
      content: null,
      savingFileName: "",
      editorOption: {
        modules: {
          toolbar: [
            ['bold', 'italic', 'underline', 'strike'],
            ['blockquote', 'code-block'],
            [{ 'header': 1 }, { 'header': 2 }],
            [{ 'list': 'ordered' }, { 'list': 'bullet' }],
            // [{ 'script': 'sub' }, { 'script': 'super' }],
            [{ 'indent': '-1' }, { 'indent': '+1' }],
            [{ 'direction': 'rtl' }],
            [{ 'size': ['small', false, 'large', 'huge'] }],
            [{ 'header': [1, 2, 3, 4, 5, 6, false] }],
            [{ 'font': [] }],
            [{ 'color': [] }, { 'background': [] }],
            [{ 'align': [] }],
            // ['clean'],
            ['link', 'image', 'video']
          ],
          syntax: {
            highlight: text => hljs.highlightAuto(text).value
          }
        }
      },
      content: dedent`
        `,
    }
  },
  methods: {
    onEditorChange: debounce(function (value) {
      this.content = value.html
    }, 466),

    download() {
      var element = document.createElement('a');
      element.setAttribute('href', 'data:text/html;charset=utf-8,' + encodeURIComponent(this.content));
      element.setAttribute('download', this.savingFileName);

      element.style.display = 'none';
      document.body.appendChild(element);

      element.click();

      document.body.removeChild(element);
    },

    readFile() {
      this.file = this.$refs.doc.files[0];
      const reader = new FileReader();
      if (this.file.name.includes(".txt") || this.file.name.includes(".html")) {
        this.savingFileName = this.file.name.replace(".txt", "").replace(".html", "");
        reader.onload = (res) => {
          this.content = res.target.result;
        };
        reader.onerror = (err) => console.log(err);
        reader.readAsText(this.file);
      } else {
        this.content = "check the console for file output";
        reader.onload = (res) => {
          console.log(res.target.result);
        };
        reader.onerror = (err) => console.log(err);
        reader.readAsText(this.file);
      }
    },
    onEditorBlur(editor) {
      console.log('editor blur!', editor)
    },
    onEditorFocus(editor) {
      console.log('editor focus!', editor)
    },
    onEditorReady(editor) {
      console.log('editor ready!', editor)
    }
  },
  computed: {
    editor() {
      return this.$refs.myTextEditor.quill
    },
    contentCode() {
      return hljs.highlightAuto(this.content).value
    }
  },
  mounted() {
    console.log('this is Quill instance:', this.editor)
  }
}
</script>

<style lang="scss" >
.example {
  display: flex;
  flex-direction: column;
  padding: 10px;

  .editor {
    height: 600px;
    margin-top: 20px ;
  }

  .output {
    width: 100%;
    height: 20rem;
    margin: 0;
    border: 1px solid #ccc;
    overflow-y: auto;
    resize: vertical;

    .code {
      padding: 1rem;
      height: 16rem;
    }

    .ql-snow {
      border-top: none;
      height: 24rem;
    }
  }
}
</style>
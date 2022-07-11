<template>
  <div>
    <Editor v-model="content" :init="init" :disabled="disabled"></Editor>
  </div>
</template>


<script>
import tinymce from "tinymce/tinymce";
import Editor from "@tinymce/tinymce-vue";
import "tinymce/themes/silver";
import "tinymce/plugins/image";
import "tinymce/plugins/media"; 
import "tinymce/plugins/table"; 
import "tinymce/plugins/link";
import "tinymce/plugins/code";
import "tinymce/plugins/lists";
import "tinymce/plugins/advlist";
import "tinymce/plugins/fullscreen";
import "tinymce/plugins/help";
import "tinymce/plugins/charmap";
import "tinymce/plugins/preview";
import "tinymce/plugins/anchor";
import "tinymce/plugins/pagebreak";
import "tinymce/plugins/searchreplace";
import "tinymce/plugins/visualblocks";
import "tinymce/plugins/visualchars";
import "tinymce/plugins/insertdatetime";
import "tinymce/plugins/nonbreaking";
import "tinymce/plugins/autosave";
import "tinymce/plugins/emoticons";
import 'tinymce/plugins/emoticons/js/emojis';
import "tinymce/plugins/quickbars";
import 'tinymce/icons/default'
import 'tinymce/themes/silver/theme' // 主题文件
import 'tinymce/icons/default'
import 'tinymce/models/dom'

// import languageUrl from "/tinymce/langs/zh-Hans.js"
// import skinUrl from "/tinymce/skins/ui/oxide"
// import contentCss from "/tinymce/skins/content/default/content.css"
export default {
  name:'tinymce-editor',
  components: {
    Editor
  },
  props: {
    value: {
      type: String,
      default: ""
    },
    disabled: {
      type: Boolean,
      default: false
    },
    imagesUploadHandler: {
      type: Function,
      default: ()=>{}
    },
    height: {
      type: Number,
      default: 770
    },
    plugins: {
      type: [String, Array],
      default:
          "preview searchreplace visualblocks visualchars fullscreen image link media code table charmap nonbreaking insertdatetime advlist lists autosave emoticons quickbars pagebreak anchor"
    },
    toolbar: {
      type: [String, Array],
      default:
          "code undo redo restoredraft | cut copy paste pastetext | forecolor backcolor bold italic underline strikethrough link | alignleft aligncenter alignright alignjustify outdent indent formatpainter | \
      styleselect formatselect fontfamily fontsize | numlist bullist  | blockquote subscript superscript removeformat | \
      emoticons table image media charmap pagebreak insertdatetime | fullscreen preview | searchreplace anchor"
    }
  },
  data() {
    return {
      //初始化配置
      init: {
        menubar: true, // 菜单栏显隐
        language_url: "/tinymce/langs/zh-Hans.js",
        language: "zh-Hans",
        skin_url: "/tinymce/skins/ui/oxide",
        min_height: 450,
        max_height: 770,
        toolbar_mode: "sliding",
        content_css:"/tinymce/skins/content/default/content.css",
        plugins: this.plugins,
        toolbar: this.toolbar,
        content_style: "p {margin: 5px 0;}",
        font_size_formats: "12px 14px 16px 18px 24px 36px 48px 56px 72px",
        font_family_formats:
            "微软雅黑=Microsoft YaHei,Helvetica Neue,PingFang SC,sans-serif;苹果苹方=PingFang SC,Microsoft YaHei,sans-serif;宋体=simsun,serif;仿宋体=FangSong,serif;黑体=SimHei,sans-serif;Arial=arial,helvetica,sans-serif;Arial Black=arial black,avant garde;Book Antiqua=book antiqua,palatino;",
        branding: false,
        // file_picker_callback: function(callback, value, meta) {
        //   console.log('未配置')
        // },
        // 图片上传
        images_upload_handler:this.imagesUploadHandler
      },
      content: this.value
    };
  },
  mounted() {
    tinymce.init({
      plugins: 'lists',
      toolbar: 'numlist bullist'
    });
  },
  methods: {

  },
  watch: {
    value(newValue) {
      this.content = newValue;
    },
    content(newValue) {
      this.$emit("input", newValue);
    }
  }
};
</script>
<style scoped lang="scss">

</style>

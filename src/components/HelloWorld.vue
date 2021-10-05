<template>
    <div class="page-one">
        <!--本地-->
        <div style="margin-top: 10px;float: left;width: 15%">
            <button @click="check">点击(本地文件)</button>
            <button @click="navigation">定位标题</button>
            <br />
            <input type="file" name="myfile" id="myfile" @change="preview($event)" style="margin-top: 40px"/>
        </div>
        <div style="float: left;width: 80%">
            <iframe v-if="showPdf" id='previewPdf' :src="'/static/pdf/web/viewer.html?file=' + fileUrl" height="800"
                    width="100%">
            </iframe>
        </div>
    </div>
</template>

<script>

    export default {
        name: 'page-one',
        data() {
            return {
                fileUrl: '',
                showPdf: false,
                contractVisable: false,
            }
        },
        methods: {
            check() {
                window.open('/static/pdf/web/viewer.html')
            },
            navigation(){
                let nav = '#[{"num":6,"gen":0},{"name":"XYZ"},90,581.25,0]'
            },
            // 这是打开本地文件进行预览
            preview(event) {
                let files = document.getElementById('myfile').files[0]
                if (files.type !== 'application/pdf') {
                    alert('只能上传一份pdf文件哦～')
                    return
                }
                this.showPdf = true
                this.fileUrl = this.getObjectURL(files)

            },
            getObjectURL(file) {
                let url = null;
                if (window.createObjectURL != undefined) { // basic
                    url = window.createObjectURL(file);
                } else if (window.webkitURL != undefined) { // webkit or chrome
                    url = window.webkitURL.createObjectURL(file);
                } else if (window.URL != undefined) { // mozilla(firefox)
                    url = window.URL.createObjectURL(file);
                }
                return url;
            },
        }
    }
</script>

<style scoped>
    .page-one button {
        margin-left: 0px;
    }
</style>

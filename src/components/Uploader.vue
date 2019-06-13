<template>
    <div class="uploader">
        <form v-on:submit.prevent="submitPhoto">
            <label>Image:</label>
            <input
                type="file"
            >
            <br>
            <label>File name:</label>
            <input
                v-model="subObj.filePath"
                type="text"
            >
            <br>
            <button>Click to Upload</button>
        </form>
    </div>
</template>

<script>
    import axios from 'axios'
    export default {
        name: 'uploader',
        data () {
            return {
                subObj: {
                    "pic": "",
                    "filePath": ""
                }
            }
        },
        methods: {
            submitPhoto(e){
                
                var file = e.target[0].files[0];
                var reader = new FileReader();
                
                reader.readAsDataURL(file);

                reader.onloadend = () => {
                    console.log('RESULT', reader.result)
                    // reader.result:      "...base64,[ACTUAL BASE64 ENCODED CODE]"
                    // delete everything before here ^
                    var start = reader.result.indexOf("base64")+7;
                    var endAnd1 = reader.result.length;
                    var encodedImg = reader.result.slice(start, endAnd1);
                    this.subObj.pic = encodedImg;
                    
                    axios.post('https://1phxrcfns0.execute-api.us-east-1.amazonaws.com/dev/upload-to-s3', this.subObj)
                    .then((response) => {
                        console.log("Success");
                        console.log(response);
                    })
                    .catch((error) => {
                        console.log("error");
                        console.log(error);
                    });
                }
                
            }
        }
    }
</script>
<template>
    <view>
        <camera class="container" :type="this.type" />
        </camera>
</template>
<script>
import * as Permissions from "expo-permissions";
import { Camera } from 'expo-camera';
export default {

    name: 'CameraScreen',
    data() {
        return {
            hasCameraPermission: false,
            type: Camera.Constants.Type.back,
        };
    },
    components: { Camera },

    mounted: function() {
        Permissions.askAsync(Permissions.CAMERA)
            .then(status => {
                hasCameraPermission = status.status == "granted" ? true : false;
            }).catch((err) => {
                console.log(err);
            });
    },
};
</script>
<style lang="css" scoped>
</style>
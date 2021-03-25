<template>
    <view>
        <touchable-opacity :on-press="getLocation">
            <text class="text-field-title">Get Location</text>
        </touchable-opacity>
        <text class="text-field-title">Location Object:</text>
        <text>{{ location }}</text>
        <text class="text-field-title">Latitude Only:</text>
        <text>{{ latitude }}</text>
        <text class="text-error">{{ errorMessage }}</text>
    </view>
</template>
<script>
import axios from 'axios'
import * as Location from "expo-location";
import * as Permissions from "expo-permissions";
export default {

    name: 'GeoLocation',

    data() {
        return {
            location: {},
            latitude: "",
            errorMessage: "",
        };
    },

    methods: {
        getLocation: function() {
            Permissions.askAsync(Permissions.LOCATION)
                .then(status => {
                    if (!status.granted) {
                        this.errorMessage = "Permission to access location was denied";
                    } else if (status.granted) {
                        Location.getCurrentPositionAsync({}).then(location => {
                            this.location = location;
                            this.latitude = location.coords.latitude
                            this.errorMessage = "";
                        });
                    }
                })
                .catch(err => {
                    console.log(err);
                }).then(() => {
                    axios.post('/api/?api_token=' + window.App.api_token, )
                        .then(r => {
                            console.log(r.data)
                            flash(r.data)
                        })
                        .catch(r => {
                            console.log(r)
                            flash(r)
                        })
                })
        },
    },
};
</script>
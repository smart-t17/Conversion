<template>
<div class="container">
    
    <div class="row">
        <b-field label="Have you already picked out a home you want to purchase with no down payment?" class="col-lg-12 text-left" custom-class="is-large"><!-- (use the Google maps API we used before) -->
            
        </b-field>
                
        
    </div>
    <b-field class="col-lg-8 text-left">
        <b-radio v-model="radioMain" native-value="YES" >
            YES
        </b-radio>
    
    </b-field>
    <b-field class="col-lg-8 text-left">
        <b-radio v-model="radioMain" native-value="NO" >
            NO
        </b-radio>
    </b-field>

    <template v-if="radioMain === 'YES'">
        <!-- // address -->
        
        <b-field label="What is the address" class="col-lg-8 text-left mt-5"><!-- (use the Google maps API we used before) -->
            <vue-google-autocomplete
                ref="address"
                id="map"
                classname="form-control"
                placeholder="Please type your address"
                v-on:placechanged="getAddressData"
            >
            </vue-google-autocomplete>
        </b-field>
        
        
        <!-- // price -->
        
        <b-field label="What is the estimated purchase price?" class="col-lg-8 text-left mt-5">
            
            <b-field>
                <b-input placeholder="0.00" icon="dollar"
                    type="number"
                    min="0.00"
                    step="0.01" value="1.00" v-model="estimatedprice">
                </b-input>
            </b-field>
        </b-field>
    
        
        <!-- // purchase -->
        
        <b-field label="Do you already have a purchase REALTOR?" class="col-lg-8 text-left mt-5">
        </b-field>
        
        <b-field class="col-lg-8 text-left">
            <b-radio v-model="radioREALTOR"
                native-value="YES">
                YES
            </b-radio>
        </b-field>
        
        <b-field class="col-lg-8 text-left">
            <b-radio v-model="radioREALTOR"
                native-value="NO">
                NO
            </b-radio>
        </b-field>

        <!-- // annual  -->
        <b-field label="What is your annual household income?" class="col-lg-8 text-left mt-5">
            <b-field>
                <b-input placeholder="0.00" icon="dollar"
                    type="number"
                    min="0.00"
                    step="0.01" value="1.00" v-model="annual">
                </b-input>
            </b-field>
            
        </b-field>
    
        <!-- // own home -->
        <b-field label="Do you already own a home?" class="col-lg-8 text-left mt-5">
                
        </b-field>
        
        <b-field class="col-lg-8 text-left">
            <b-radio v-model="radioHome"
                native-value="YES">
                YES
            </b-radio>
        </b-field>

        <template v-if="radioHome === 'YES'">
            <b-field class="col-lg-8 text-left ml-5">
                <b-radio v-model="radioPrimaryHome"
                    native-value="YES">
                    Primary home
                </b-radio>
            </b-field>
            
            <b-field class="col-lg-8 text-left ml-5">
                <b-radio v-model="radioPrimaryHome"
                    native-value="NO">
                    Investment home
                </b-radio>
            </b-field>
        </template>

        <b-field class="col-lg-8 text-left">
            <b-radio v-model="radioHome"
                native-value="NO">
                NO
            </b-radio>
        </b-field>
        
        <!--  veteran -->
        <b-field label="Are you a veteran?" class="col-lg-8 text-left mt-5">
        </b-field>
                    
        <b-field class="col-lg-8 text-left">
            <b-radio v-model="radioVeteran"
                native-value="YES">
                YES
            </b-radio>
        </b-field>

        <template v-if="radioVeteran === 'YES'">

            <b-field label="Do you have a service related disability?" class="col-lg-8 text-left ml-5">
            </b-field>
            
            <b-field class="col-lg-8 text-left ml-5">
                <b-radio v-model="radioDisability"
                    native-value="YES">
                    YES
                </b-radio>
            </b-field>

            <b-field class="col-lg-8 text-left ml-5">
                <b-radio v-model="radioDisability"
                    native-value="NO">
                    NO
                </b-radio>
            </b-field>
        </template>

        <b-field class="col-lg-8 text-left">
            <b-radio v-model="radioVeteran"
                native-value="NO">
                NO
            </b-radio>
        </b-field>
        
        <!-- firstname -->
        
        <b-field horizontal label="First name" class="col-lg-7 text-left mt-5">
            <b-input  v-model="firstname"></b-input>
        </b-field>
    
        <b-field horizontal label="Last name" class="col-lg-7 text-left">
            <b-input v-model="lastname"></b-input>
        </b-field>
    
        <!-- // phone number -->
        <b-field horizontal label="Phone number" class="col-lg-7 text-left">
            <b-input v-model="phonenumber"></b-input>
        </b-field>

        <!-- // email address -->
        <b-field horizontal label="Email address" class="col-lg-7 text-left">
            <b-input placeholder="Email"
                type="email" v-model="emailaddress"></b-input>
        </b-field>

    </template>

    <!-- //////////////// NO ///////////////// -->
    <template v-else-if="radioMain === 'NO'">

        <!-- county -->
        
        <b-field label="What county do you want to buy in?" class="col-lg-8 text-left mt-5">
            <b-select placeholder="Select County" v-model="selectedCounty">
                <option v-for="(county, index) in arrayOfCounty" :key="index" :value="county.name">{{county.name}}</option>

            </b-select>
        </b-field>
        <!-- approximate purchase price -->

        <b-field label="How much is the approximate purchase price of the home you want to buy?" class="col-lg-8 text-left mt-5">
            <b-field>
                <b-input placeholder="0.00" icon="dollar"
                    type="number"
                    min="0.00"
                    step="0.01" value="1.00" v-model="approximateprice">
                </b-input>
            </b-field>

        </b-field>

        <!-- // purchase realtor -->
        
        <b-field label="Do you already have a purchase REALTOR?" class="col-lg-8 text-left mt-5">
        </b-field>
    
        <b-field class="col-lg-8 text-left">
            <b-radio v-model="radioREALTOR"
                native-value="YES">
                YES
            </b-radio>
        </b-field>
        <b-field class="col-lg-8 text-left">
            <b-radio v-model="radioREALTOR"
                native-value="NO">
                NO
            </b-radio>
        </b-field>
        
        <!-- // annual  -->
        <b-field label="What is your annual household income?" class="col-lg-8 text-left mt-5">
            <b-field>
                <b-input placeholder="0.00" icon="dollar"
                    type="number"
                    min="0.00"
                    step="0.01" value="1.00" v-model="annual">
                </b-input>
            </b-field>
        </b-field>
    
        <!-- // own home -->
        <b-field label="Do you already own a home?" class="col-lg-8 text-left mt-5">
                
        </b-field>
                
    
        <b-field class="col-lg-8 text-left">
            <b-radio v-model="radioHome"
                native-value="YES">
                YES
            </b-radio>
        </b-field>

        <template v-if="radioHome === 'YES'">
            <b-field class="col-lg-8 text-left ml-5">
                <b-radio v-model="radioPrimaryHome"
                    native-value="YES">
                    Primary home
                </b-radio>
            </b-field>
            <b-field class="col-lg-8 text-left ml-5">
                <b-radio v-model="radioPrimaryHome"
                    native-value="NO">
                    Investment home
                </b-radio>
            </b-field>
        </template>

        <b-field class="col-lg-8 text-left">
            <b-radio v-model="radioHome"
                native-value="NO">
                NO
            </b-radio>
        </b-field>

        <!--  veteran -->
        
        <b-field label="Are you a veteran?" class="col-lg-8 text-left mt-5">
                
        </b-field>
                
        <b-field class="col-lg-8 text-left">
            <b-radio v-model="radioVeteran"
                native-value="YES">
                YES
            </b-radio>
        </b-field>

        <template v-if="radioVeteran === 'YES'">

            <b-field label="Do you have a service related disability?" class="col-lg-8 text-left ml-5">
                    
            </b-field>

            <b-field class="col-lg-8 text-left ml-5">
                <b-radio v-model="radioDisability"
                    native-value="YES">
                    YES
                </b-radio>
            </b-field>
            <b-field class="col-lg-8 text-left ml-5">
                <b-radio v-model="radioDisability"
                    native-value="NO">
                    NO
                </b-radio>
            </b-field>
        </template>

        <b-field class="col-lg-8 text-left">
            <b-radio v-model="radioVeteran"
                native-value="NO">
                NO
            </b-radio>
        </b-field>

        
        
        <!-- firstname -->
        <b-field horizontal label="First name" class="col-lg-7 text-left mt-5">
            <b-input  v-model="firstname"></b-input>
        </b-field>
    
        <b-field horizontal label="Last name" class="col-lg-7 text-left">
            <b-input v-model="lastname"></b-input>
        </b-field>
    
        <!-- // phone number -->
        <b-field horizontal label="Phone number" class="col-lg-7 text-left">
            <b-input v-model="phonenumber"></b-input>
        </b-field>

        <!-- // email address -->
        <b-field horizontal label="Email address" class="col-lg-7 text-left">
        <b-input v-model="emailaddress"></b-input>
        </b-field>
    </template>
    <template >
        
    </template>

    
    <b-message type="is-success" class="col-lg-8" v-if="radioMain === 'none'">
        To continue, please select above option
    </b-message>
    <b-field class="col-lg-7 text-right" v-else>
        <button type="submit" class="button" @click="postPost">Submit</button>
    </b-field>

        
</div>
</template>

<script>
import VueGoogleAutocomplete from 'vue-google-autocomplete'
export default {
    name: 'Questions',
    created() {
    },
    data() {
        return {
            radioMain: '',
            radioREALTOR: '',
            radioHome: '',
            radioPrimaryHome: '',
            radioVeteran : '',
            radioDisability : '',
            address: '',
            postBody: '',
            errors: [],
            emailaddress : '',
            firstname : '',
            lastname : '',
            phonenumber : '',
            estimatedprice : '',
            annual : '',
            approximateprice : '',
            selectedCounty : {name:"None"},
            arrayOfCounty : [ {name:'Alameda'}, {name:'Alpine'}, {name:'Amador'}, {name:'Butte'}, {name:'Calaveras'}, {name:'Colusa'}, {name:'Contra Costa'}, {name:'Del Norte'}, {name:'El Dorado'}, {name:'Fresno'}, {name:'Glenn'}, {name:'Humboldt'}, {name:'Imperial'}, {name:'Inyo'}, {name:'Kern'}, {name:'Kings'}, {name:'Lake'}, {name:'Lassen'}, {name:'Los Angeles'}, {name:'Madera'}, {name:'Marin'}, {name:'Mariposa'}, {name:'Mendocino'}, {name:'Merced'}, {name:'Modoc'}, {name:'Mono'}, {name:'Monterey'}, {name:'Napa'}, {name:'Nevada'}, {name:'Orange'}, {name:'Placer'}, {name:'Plumas'}, {name:'Riverside'}, {name:'Sacramento'}, {name:'San Benito'}, {name:'San Bernardino'}, {name:'San Diego'}, {name:'San Francisco'}, {name:'San Joaquin'}, {name:'San Luis Obispo'}, {name:'San Mateo'}, {name:'Santa Barbara'}, {name:'Santa Clara'}, {name:'Santa Cruz'}, {name:'Shasta'}, {name:'Sierra'}, {name:'Siskiyou'}, {name:'Solano'}, {name:'Sonoma'}, {name:'Stanislaus'}, {name:'Sutter'}, {name:'Tehama'}, {name:'Trinity'}, {name:'Tulare'}, {name:'Tuolumne'}, {name:'Ventura'}, {name:'Yolo'}, {name:'Yuba'}],
        
            
        }
    },
    components: {
        VueGoogleAutocomplete,
    },
    methods: {
        /**
        * When the location found
        * @param {Object} addressData Data of the found location
        * @param {Object} placeResultData PlaceResult object
        * @param {String} id Input container ID
        */
        getAddressData: function (addressData, placeResultData, id) {
            this.address = addressData;
        },
        alert(response) {
            this.$dialog.alert(response)
            
        },
        // Pushes posts to the server when called.
        postPost() {
                        
            if (this.radioMain === 'YES') {
                this.postBody = { "mainpurchase" : this.radioMain, "address": this.address, "price" : this.estimatedprice, "realtor" : this.radioREALTOR, "annual" : this.annual, "ownhome" : this.radioHome, "hometype" : this.radioPrimaryHome, "veteran" : this.radioVeteran, "disability" : this.radioDisability, "firstname" : this.firstname, "lastname" : this.lastname, "phonenumber" : this.phonenumber, "emailaddress" : this.emailaddress} 
            }else {
                this.postBody = { "mainpurchase" : this.radioMain, "county": this.selectedCounty, "price" : this.approximateprice, "realtor" : this.radioREALTOR, "annual" : this.annual, "ownhome" : this.radioHome, "hometype" : this.radioPrimaryHome, "veteran" : this.radioVeteran, "disability" : this.radioDisability, "firstname" : this.firstname, "lastname" : this.lastname, "phonenumber" : this.phonenumber, "emailaddress" : this.emailaddress}
            }
            this.$http.post('http://downpaymentlookup.com/sendemail.php', {
            body: this.postBody
            })
            .then(response => {
                this.alert(response)

            })
            .catch(e => {
            this.errors.push(e)
            })

        }
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.button{
  background: #50d8af;
  border: 0;
  border-radius: 3px;
  color: #fff;
  transition: 0.4s;
  cursor: pointer;
}
</style>

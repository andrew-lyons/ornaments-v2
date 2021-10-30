<template>
    <div class="inputs">
        <div class="inputs-form" :class="completed
                                    ? success
                                        ? 'green'
                                        : 'red'
                                    : ''">
            <div v-if="!completed">
                <div class="inputs-form-row desktop">
                    <div class="inputs-form-row-left">
                        <h4>Option</h4>
                        
                        <select v-model="option">
                            <option value="">--Please choose an option--</option>
                            <option value="Full Name">Full Name</option>
                            <option value="Family Name">Family Name</option>
                            <option value="Anonymous">Anonymous</option>
                        </select>
                    </div>

                    <div class="inputs-form-row-right">
                        <h4>Name</h4>
                        <input type="text" :disabled="option == 'Anonymous' || option == ''" v-model="fullName">
                    </div>
                </div>

                <div class="inputs-form-row mobile">
                    <div class="inputs-form-row-full">
                        <h4>Option</h4>
                        
                        <select v-model="option">
                            <option value="">--Please choose an option--</option>
                            <option value="Full Name">Full Name</option>
                            <option value="Family Name">Family Name</option>
                            <option value="Anonymous">Anonymous</option>
                        </select>
                    </div>
                </div>

                <div class="inputs-form-row mobile">
                    <div class="inputs-form-row-full">
                        <h4>Name</h4>
                        <input type="text" :disabled="option == 'Anonymous' || option == ''" v-model="fullName">
                    </div>
                </div>

                <div class="inputs-form-row">
                    <div class="inputs-form-row-full">
                        <h4>Email</h4>
                        <input type="text" placeholder="example@gmail.com" v-model="email">
                    </div>
                </div>

                <div class="inputs-form-row">
                    <div class="inputs-form-row-full">
                        <h4>Name or Nickname of Baby</h4>
                        <input type="text" :disabled="(_props.curId == 3)" placeholder="Nora Marjorie, Baby Smith, My Angel, etc." v-model="babyName">
                    </div>
                </div>

                <div class="inputs-form-row">
                    <div class="inputs-form-row-full">
                        <h4>Date (or Dates)</h4>
                        <input type="text" :disabled="(_props.curId == 3)" placeholder="10/3/2021, 10/3/2021 - 10/5/2021, etc." v-model="dateInfo">
                    </div>
                </div>

                <div class="inputs-form-row">
                    <div class="inputs-form-row-full">
                        <h4>Local Pickup / Mail</h4>
                        <div class="mailer">
                            <input type="checkbox" :disabled="mail" v-model="local">Local
                            <input type="checkbox" :disabled="local" id="mailbox" v-model="mail"><span id="mail">Mail</span>
                            <input type="text" :disabled="!mail" placeholder="Mailing Address" v-model="address">
                        </div>
                    </div>
                </div>

                <div class="inputs-form-row">
                    <div class="errors" v-if="showErrors">
                        <h6 v-for="(err, index) in errors" :key="err + index">{{err}}</h6>
                    </div>
                </div>

                <div :class="processing && 'processing'">
                    <div class="lds-dual-ring" v-if="processing">
                        
                    </div>
                    <StripeStuff @charge="charge" />
                </div>
                
            </div>
            <div v-else>
                <div class="inputs-form-row">
                    <div class="inputs-form-row-full">
                        <h2>{{success ? 'Success! Thank you so much for your donation.' : 'Something went wrong...'}}</h2>
                        <h2 v-if="!success">{{message}}</h2>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import StripeStuff from './StripeStuff.vue'

export default {
    name: "Form",
    components: { StripeStuff },
    props: {
        curId: { required: false }
    },
    data() {
        return {
            option: '',
            fullName: '',
            email: '',
            address: '',
            babyName: '',
            dateInfo: '',
            local: false,
            mail: false,
            errors: {
                ers: []
            },
            showErrors: false,
            completed: false,
            success: false,
            message: '',
            processing: false
        }
    },
    methods: {
        validate() {
            this.errors = []

            // no option chosen
            this.option == "" && this.errors.push("No option selected")

            // option chosen and no name given
            if (this.option != "") {
                if (this.option != "Anonymous") {
                    this.fullName.length == 0 && this.errors.push("No name given")
                }
            }

            // invalid email
            !this.validateEmail(this.email) && this.errors.push("Invalid email")

            // if we need a baby name and dates
            if (this._props.curId != 3) {
                // no baby name
                this.babyName.length == 0 && this.errors.push("No baby name given")

                // no dates
                this.dateInfo.length == 0 && this.errors.push("No dates provided")
            }

            if (!this.local) {
                if (!this.mail) {
                    this.errors.push("Select local or mail")
                }
                else if (this.mail) {
                    this.address.length == 0 && this.errors.push("No address given")
                }
            }

            this.showErrors = this.errors.length > 0

            return this.errors.length == 0
        },
        charge(params) {
            if (this.validate()) {
                const misc = `baby: ${this.babyName}, date(s): ${this.dateInfo}, address: ${this.address}, local: ${this.local}, mail: ${this.mail}`

                const data = {
                    card: params[0],
                    other: {
                        name: this.option == 'Anonymous' ? 'Anonymous' : this.fullName,
                        email: this.email,
                        description: misc,
                        amount: params[1]
                    }
                }

                console.log(params, data)

                const url = "https://express-nora.herokuapp.com/charge"

                const options = {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify(data)
                }

                this.processing = true

                fetch(url, options)
                .then(res => res.json())
                .then((data) => {
                    if (data.success) {
                        this.completed = true
                        this.success = true
                        this.processing = false
                        this.message = data.message
                    }
                    else {
                        this.completed = true
                        this.success = false
                        this.processing = false
                        this.message = data.message.code
                    }
                })
                .catch(err => console.log('err: ', err))
            }
        },
        error(error) {
            console.log(error)
        },
        validateEmail(email) {
            const re = /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
            return re.test(String(email).toLowerCase());
        }
    }
}
</script>

<style lang="scss" scoped>
    .desktop {
        @media only screen and (max-width: 1024px) {
            display: none !important;
        }
    }

    .mobile {
        @media only screen and (min-width: 1025px) {
            display: none !important;
        }
    }

    .green {
        background-color: lightgreen !important;
    }

    .red {
        background-color: lightcoral !important;
    }

    .processing {
        opacity: 0.5;
        position: relative;
        pointer-events: none;

        .lds-dual-ring {
            position: absolute;
            top: 25%;
            left: 40%;

            display: inline-block;
            width: 80px;
            height: 80px;

            &:after {
                content: " ";
                display: block;
                width: 64px;
                height: 64px;
                margin: 8px;
                border-radius: 50%;
                border: 6px solid #000;
                border-color: #000 transparent #000 transparent;
                animation: lds-dual-ring 1.2s linear infinite;
            }

            @keyframes lds-dual-ring {
                0% {
                    transform: rotate(0deg);
                }
                100% {
                    transform: rotate(360deg);
                }
            }
        }
    }

    .errors {
        display: flex;
        color: red;

        h6 {
            padding: 0 6px;
        }
    }

    .inputs {
        display: flex;
        align-items: center;
        justify-content: center;
        width: 50%;

        @media only screen and (max-width: 1360px) {
            width: 66%;
        }

        @media only screen and (max-width: 1024px) {
            width: 100%;
        }

        &-form {
            width: 100%;
            margin: 50px;
            padding: 50px;
            background-color: white;
            border-radius: 8px;
            box-shadow: grey 5px 6px 15px 0px;

            @media only screen and (max-width: 1360px) {
                padding: 50px;
            }

            @media only screen and (max-width: 1024px) {
                margin: 50px 24px 24px;
            }

            @media only screen and (max-width: 640px) {
                padding: 24px;
            }

            &-row {
                display: flex;
                flex-wrap: nowrap;

                &-left, &-right, &-full {
                    width: 100%;

                    h4 {
                        margin-top: 3px;
                        margin-bottom: 6px;
                    }

                    & input[type=text] {
                        width: calc(100% - 14px);
                        height: 24px;
                        font-family: 'Quicksand', sans-serif;
                        padding-left: 8px;
                    }

                    select {
                        width: 100%;
                        height: 30px;
                        font-family: 'Quicksand', sans-serif;
                    }
                }

                &-full {
                    margin: 6px 0;

                    .card {
                        display: flex;
                        width: 100%;

                        #one, #yy {
                            margin-right: 12px;
                        }

                        #mm, #yy, #cvv {
                            width: 32px;
                        }
                    }

                    .mailer {
                        display: flex;
                        align-items: center;

                        #mail {
                            margin-right: 12px;
                        }

                        #mailbox {
                            margin-left: 12px;
                        }
                    }

                    .donation {
                        display: flex;
                        align-items: center;

                        #amount {
                            width: 50%;
                            margin-right: 12px;
                        }

                        #cta {
                            width: 50%;
                            padding: 4px 0;
                            border-radius: 8px;
                            text-align: center;
                            box-shadow: black 1px 1px 1px 1px;
                            background-color: lightgreen;
                            cursor: pointer;
                            transition: opacity 0.3s;

                            &:hover {
                                opacity: .8;
                            }
                        }
                    }
                }

                &-left {
                    margin: 6px 6px 6px 0;
                }

                &-right {
                    margin: 6px 0 6px 6px;
                }
            }

            .separator {
                margin-top: 36px;
                margin-bottom: 6px;
            }
        }
    }
</style>
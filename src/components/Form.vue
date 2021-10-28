<template>
    <div class="inputs">
        <div class="inputs-form">
            <div class="inputs-form-row">
                <div class="inputs-form-row-left">
                    <h4>First Name</h4>
                    <input type="text" placeholder="John">
                </div>

                <div class="inputs-form-row-right">
                    <h4>Last Name</h4>
                    <input type="text" placeholder="Doe">
                </div>
            </div>

            <div class="inputs-form-row">
                <div class="inputs-form-row-full">
                    <h4>Email</h4>
                    <input type="text" placeholder="example@gmail.com">
                </div>
            </div>

            <div class="inputs-form-row">
                <div class="inputs-form-row-full">
                    <h4>Name or Nickname of Baby</h4>
                    <input type="text" placeholder="Nora Marjorie, Baby Smith, My Angel, etc.">
                </div>
            </div>

            <div class="inputs-form-row">
                <div class="inputs-form-row-full">
                    <h4>Date (or Dates)</h4>
                    <input type="text" placeholder="10/3/2021, 10/3/2021 - 10/5/2021, etc.">
                </div>
            </div>

            <div class="inputs-form-row">
                <div class="inputs-form-row-full">
                    <h4>Supporter Name or Family Name</h4>
                    <input disabled type="text" placeholder="Andrew, The Lyons Family, etc.">
                </div>
            </div>

            <div class="inputs-form-row">
                <div class="inputs-form-row-full">
                    <h4>Local Pickup / Mail (If local, please leave an email for us)</h4>
                    <div class="mailer">
                        <input type="checkbox">Local
                        <input type="checkbox" id="mailbox"><span id="mail">Mail</span>
                        <input type="text" placeholder="Mailing Address">
                    </div>
                </div>
            </div>

            <h3 class="separator">Card Information</h3>

            <StripeStuff />
        </div>
    </div>
</template>

<script>
import StripeStuff from './StripeStuff.vue'

export default {
    name: "Form",
    components: { StripeStuff }
}
</script>

<style lang="scss" scoped>
    .inputs {
        width: 50%;

        &-form {
            margin: 50px;
            padding: 25px 40px;

            background-color: white;
            border-radius: 8px;
            box-shadow: black 1px 1px 1px 1px;

            &-row {
                display: flex;
                flex-wrap: nowrap;

                &-left, &-right, &-full {
                    width: 100%;

                    h4 {
                        margin-top: 3px;
                        margin-bottom: 3px;
                    }

                    & input[type=text] {
                        width: calc(100% - 14px);
                        height: 24px;
                        font-family: 'Quicksand', sans-serif;
                        padding-left: 8px;
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
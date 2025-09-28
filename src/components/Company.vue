<script setup lang="ts">
    import { ref } from 'vue'
    import bg from './images/bg.png'
    import CAngryT from './images/CAngryT.png'
    import Cat from './images/Cat.png'
    import Ellipse from './images/Ellipse.png'

    const balance = ref('100 BNB')
    const wallet = ref('0x23B067aB65C16Eb9e0917F475E7883Fbd4f18f7f')

    const shortenAddress = (address: string, chars = 4): string => {
        if (!address) return ""
        const start = address.slice(0, chars + 2) 
        const end = address.slice(-chars)
        return `${start}...${end}`
    }
</script>

<template>
    <div class="top-section">
        <img :src="bg" alt="bg" class="bg">
        <header>
            <img :src="CAngryT" alt="CAngryTlogo">
            <div class="connect">
                <div class="balance">
                    <span>Wallet balance:</span>
                    <p>{{ balance }}</p>
                </div>
                <button class="wallet">{{ shortenAddress(wallet) }}</button>
            </div>
        </header>
        <div class="welcome">
            <div class="greeting">
                <h2>Hi ! It seems I`m <span>kindness</span> </h2>
                <p>but who knows</p>
                <button>Let’s meet -></button>
            </div>
            <div class="company-ava">
                <img :src="Cat" alt="bg" class="cat">
                <img :src="Ellipse" alt="kot" class="bg">
            </div>
        </div>
    </div>
</template>

<style scoped>
    .top-section {
        /* width: 100%; */
        padding: 0 24px; 
        position: relative;
        .bg {
            position: absolute;
            width: 100%;
            margin: 0;
        }
        header {
            width: 100%;
            border: 2px solid black;
            width: 100%;
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-top: 24px;
            .logo {
                border: 2px solid black;
            }
            .connect {
                size: 324px 48px;
                border: 2px solid black;
                display: flex;
                justify-content: space-between;
                align-items: center;
                .balance {
                    width: 145px;
                    display: flex;
                    flex-direction: column;
                    justify-content: space-between;
                    align-items: center;
                    padding: 7px 24px;
                    border: 1px solid #E6E6E6;
                    background-color: #FAFAFA;
                    border-radius: 200px;
                    span {
                        font-size: 14px;
                        font-weight: 300;
                        line-height: 150%;
                    }
                    p {
                        font-size: 16px;
                        font-weight: 800;
                        line-height: 150%;
                    }
                }
                .wallet {
                    width: 163px;
                    padding: 16px 24px;
                    border: 1px solid #E6E6E6;
                    background-color: #FAFAFA;
                    border-radius: 200px;
                }
            }
        }
        div.welcome {
            width: 100%;
            padding: 100px 0px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            gap: 100px;
            .greeting {
                width: 534px;
                display: flex;
                flex-direction: column;
                justify-content: center;
                align-items: start;
                h2 {
                    padding: 0;
                    margin: 0;
                    font-size: 72px;
                    font-weight: 700;
                    line-height: 72px;
                    span {
                        font-size: 72px;
                        font-weight: 700;
                        line-height: 72px;
                        color: #E9B800
                    }
                }
                p {
                    font-size: 24px;
                    color: #9D9D9D;
                    font-weight: 400;
                    line-height: 16px;
                }
                button {

                }
            }
            .company-ava {
                border: 2px solid black;
                display: flex;
                justify-content: center;
                align-items: center;
                position: relative;

                .cat {
                    z-index: 100;
                    position: absolute;
                }
                .bg {
                
                }
            }
        }
    }
</style>
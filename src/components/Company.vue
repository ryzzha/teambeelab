<script setup lang="ts">
    import { ref } from 'vue'
    import CAngryT from './images/CAngryT.png'
    import Cat from './images/Cat.png'
    import Ellipse from './images/Ellipse.png'
    import arrowDown from './images/arrowDown.png'
    import menu from './images/menu.png'

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
        <header>
            <img :src="CAngryT" alt="CAngryTlogo">
            <div class="connect">
                <div class="balance">
                    <span>Wallet balance:</span>
                    <p>{{ balance }}</p>
                </div>
                <button class="wallet">{{ shortenAddress(wallet) }} <img :src="arrowDown" alt="arrow"></button>
            </div>
            <div class="menu">
                <img :src="menu" alt="menu">
            </div>
        </header>
        <div class="welcome">
            <div class="greeting">
                <h2>Hi ! It seems I`m <span>kindness</span> </h2>
                <p>but who knows</p>
                <button>Let’s meet ➔</button>
            </div>
            <div class="company-ava">
                <img :src="Ellipse" alt="ellipse" class="ellipse">
                <img :src="Cat" alt="cat" class="cat">
            </div>
        </div>
    </div>
</template>

<style scoped>
    .top-section {
        width: 100vw;            
        margin: 0 auto;
        display: flex;
        flex-direction: column;
        align-items: center;
        header {
            width: 100%;
            width: 100%;
            display: flex;
            justify-content: space-between;
            align-items: center;
            .logo {
            }
            .connect {
                size: 324px 47px;
                display: flex;
                justify-content: space-between;
                align-items: center;
                gap: 20px;
                .balance {
                    width: 152px;
                    display: flex;
                    flex-direction: column;
                    justify-content: space-between;
                    align-items: start;
                    padding: 7px 24px;
                    border: 1px solid #E6E6E6;
                    background-color: #FAFAFA;
                    border-radius: 200px;
                    span {
                        font-size: 14px;
                        font-weight: 300;
                        line-height: 100%;
                        color: #333333;
                    }
                    p {
                        margin: 0;
                        font-size: 16px;
                        font-weight: 600;
                        line-height: 100%;
                    }
                }
                .wallet {
                    width: 165px;
                    padding: 16px 24px;
                    border: 1px solid #E6E6E6;
                    background-color: #FAFAFA;
                    color: #C5FFF0;
                    border-radius: 200px;
                    img {
                        margin-left: 3px;
                    }
                }
            }
            .menu {
                display: none;
            }
        }
        div.welcome {
            width: 100%;
            height: 100%;
            display: flex;
            justify-content: start;
            .greeting {
                display: flex;
                flex-direction: column;
                justify-content: center;
                align-items: start;
                h2 {
                    padding: 0;
                    margin: 0;
                    text-align: left;
                    span {
                        color: #E9B800
                    }
                }
                p {
                    color: #9D9D9D;
                }
                button {
                    height: 50px;
                    border-radius: 50px;
                    background-color: #FFFFFF;
                    border: 1px solid #E6E6E6;
                    box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);
                }
            }
            .company-ava {
                display: flex;
                justify-content: start;
                align-items: center;
                gap: 100px;

                .cat {
                    height: auto;  
                    z-index: 100;
                    position: absolute;
                }
                .ellipse {
                    z-index: 10;
                }
            }
        }
    }
    @media (min-width: 768px) { 
        .top-section {
            background-image: url('./images/bg.png');
            height: 100vh; 
            width: 100%;
            padding: 0 200px; 
            header {
                margin-top: 24px;
                .logo {

                }
                .connect {
                    
                }

            }
            .welcome {
                align-items: center;
                gap: 35%;
                text-align: center;     
                padding: 100px 0px;
                .greeting {
                    width: 35%;
                    h2 {
                        font-size: 77px;
                        font-weight: 700;
                        line-height: 77px;
                        span {
                            font-size: 77px;
                            font-weight: 700;
                            line-height: 77px;
                        }
                    }
                    p {
                        font-size: 24px;
                        font-weight: 400;
                        line-height: 16px;
                    }
                    button {
                        width: 300px;
                        margin-top: 25px;
                        font-size: 24px;
                        font-weight: 500;
                        line-height: 16px;
                    }
                }
                .company-ava {
                    size: 400px 400px;
                    position: relative;
                    .cat {
                        width: 100%; 
                    }
                } 
            }
        }
    }
    @media (max-width: 768px) { 
        .top-section {
            background-image: url('./images/bgMob.png');
            background-position: start;
            height: 45vh; 
            width: 100%;
            padding: 0px 30px; 
            header {
                margin-top: 10px;
                .logo {

                }
                .connect {
                    display: none;
                }
                .menu {
                    width: 32px;
                    height: 32px;
                    display: flex;
                    justify-content: center;
                    align-items: center;
                    width: 32px;
                    height: 32px;
                    background-color: #FBFBFE;
                    border-radius: 50%; 
                    cursor: pointer;
                    box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.15);
                }
            }
            .welcome {
                flex-direction: column;  
                align-items: start;
                gap: 1px;
                text-align: center;     
                padding: 25px 0px;
                .greeting {
                    order: 2;
                    h2 {
                        width: 65%;
                        font-size: 42px;
                        font-weight: 700;
                        line-height: 42px;
                        span {
                            font-size: 42px;
                            font-weight: 700;
                            line-height: 42px;
                        }
                    }
                    p {
                        font-size: 16px;
                        font-weight: 400;
                        line-height: 16px;
                    }
                    button {
                        min-width: 95%;
                        margin-top: 20px;
                        align-self: center;
                        font-size: 16px;
                        font-weight: 500;
                        line-height: 16px;
                    }
                }
                .company-ava {
                    size: 200px 200px;
                    order: 1;
                    align-self: center;
                    .cat {
                        width: 201px; 
                        z-index: 100;
                        position: absolute;
                    }
                    .ellipse {
                        width: 203px; 
                    }
                } 
            }
        }
    }
</style>
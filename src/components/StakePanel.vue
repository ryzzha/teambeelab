<script setup lang="ts">
import { onMounted, reactive } from 'vue';
import BIN from './images/BIN.png'
import warning from './images/warning.png'

interface DailyMetric {
  stakingDays: number;
  incomeDay: number;
  incomePeriod: number;
  expected: number;
  status: 'Активний' | 'Неактивний';
}

interface UserStats {
  staked: number;
  rebonded: number;
  binSolded: number;
  binClaimed: number;
}

const mockUserStats: UserStats = {
    staked: 25,
    rebonded: 10,
    binSolded: 360,
    binClaimed: 7660
}

const mockDailyMetric: DailyMetric[] = [
    {
        stakingDays: 17,
        incomeDay: 0.5,
        incomePeriod: 31.7,
        expected: 10,
        status: 'Активний'
    },
    {
        stakingDays: 17,
        incomeDay: 0.5,
        incomePeriod: 31.7,
        expected: 10,
        status: 'Неактивний'
    },
    {
        stakingDays: 17,
        incomeDay: 0.5,
        incomePeriod: 31.7,
        expected: 10,
        status: 'Активний' 
    }
]

const userStats = reactive<UserStats>({
    staked: 0,
    rebonded: 0,
    binSolded: 0,
    binClaimed: 0
});

let dailyMetrics = reactive<DailyMetric[]>([]);

const fetchStats = async () => {
    try {
        const res = await new Promise<UserStats>((resolve) => resolve(mockUserStats)).then((res) => res);
        userStats.staked = res.staked;
        userStats.rebonded = res.rebonded;
        userStats.binSolded = res.binSolded;
        userStats.binClaimed = res.binClaimed;
    } catch(err) {
        console.error(err)
    }
}

const fetchMetric = async () => {
    try {
        const res = await new Promise<DailyMetric[]>((resolve) => resolve(mockDailyMetric)).then((res) => res);
        dailyMetrics = res;
    } catch(err) {
        console.error(err)
    }
}

onMounted(() => {
    fetchStats();
    fetchMetric();
})

</script>

<template>
    <main>
        <section class="stake-panel">
            <div class="stats">
                <div class="staked">
                    <p>Всього застекано</p>
                    <span><img :src="BIN" alt="bin"> {{ userStats.staked }} BIN</span>
                    <p><img :src="warning" alt="warn"> Максимальний дохід по стекінгу 200%</p>
                </div>
                <div class="other">
                    <div>
                        <p>Ребондіровано</p>
                        <span>{{ userStats.rebonded }} BIN</span>
                    </div>
                    <div>
                        <p>Продано BIN</p>
                        <span>{{ userStats.binSolded }} BIN</span>
                    </div>
                    <div>
                        <p>Заклеймено BIN</p>
                        <span>{{ userStats.binClaimed }} BIN</span>
                    </div>
                </div>
            </div>
            <ul class="history">
                <li class="fields">
                    <span>Дні стекінгу</span>
                    <span>Дохід за день</span>
                    <span>Дохід за період</span>
                    <span>Очікується</span>
                    <span>Статус</span>
                </li>
                <li class="metric" v-for="metric in dailyMetrics">
                    <div><span class="field">Дні стекінгу:</span>{{ metric.stakingDays }} днів</div>
                    <div><span class="field">Дохід за день:</span>{{ metric.incomeDay }} %</div>
                    <div><span class="field">Дохід за період:</span>{{ metric.incomePeriod }} %</div>
                    <div><span class="field">Очікується:</span>{{ metric.expected }} BIN</div>
                    <div>
                        <span class="field">Статус</span>
                        <span
                            class="status"
                            :class="{
                                active: metric.status === 'Активний',
                                completed: metric.status === 'Неактивний'
                            }"
                        >{{ metric.status }}</span>
                    </div>
                </li>
            </ul>   
        </section>
    </main>
</template>

<style scoped>
    main {
        width: 100%;
        display: flex;
        flex-direction: column;
        justify-content: start;
        align-items: center;
        section.stake-panel {
            border-radius: 16px;
            border: 1px solid #E6E6E6;
            .stats {
                width: 100%;
                display: flex;
                justify-content: space-between;
                align-items: center;
                .staked {
                    width: 40%;
                    padding: 10px;
                    display: flex;
                    flex-direction: column;
                    justify-content: space-between;
                    align-items: start;
                    p:first-child {
                        font-size: 15px;
                        font-weight: 500;
                        line-height: 20px;
                    }
                    span {
                        font-size: 52px;
                        font-weight: 700;
                        line-height: 62px;
                        letter-spacing: 0;
                        display: flex;
                        img {
                            margin-right: 10px;
                        }
                    }
                    p {
                        font-size: 13px;
                        font-weight: 400;
                        line-height: 150%;
                        letter-spacing: 0;
                        display: flex;
                        align-items: center;
                        gap: 5px;
                    }
                }
                .other {
                    width: 60%;
                    padding: 10px;
                    display: flex;
                    flex-direction: column;
                    justify-content: space-between;
                    align-items: start;
                    div {
                        width: 100%;
                        padding: 10px;
                        display: flex;
                        justify-content: space-between;
                        align-items: center;
                        font-size: 18px;
                        font-weight: 400;
                        line-height: 0;
                        letter-spacing: 0;
                        border-top: 1px solid #E6E6E6;
                        border-bottom: 1px solid #E6E6E6;
                        &:first-child {
                            border-top: none;
                        }
                        &:last-child {
                            border-bottom: none;
                        }
                    }
                }
            }

            .history {
                .fields {
                    display: flex;
                    justify-content: space-between;
                    align-items: center;
                    padding: 30px 20px;
                    font-size: 15px;
                    font-weight: 400;
                    line-height: 100%;
                    letter-spacing: 0;
                    color: #00000080;
                    border-top: 1px solid #E6E6E6;
                    border-bottom: 1px solid #E6E6E6;
                    span {
                        flex: 1; 
                        text-align: start; 
                    }
                }
                .metric {
                    display: flex;
                    justify-content: space-between;
                    align-items: center;
                    padding: 20px;
                    border-top: 1px solid #E6E6E6;
                    border-bottom: 1px solid #E6E6E6;
                    div {
                        flex: 1; 
                        text-align: start; 
                    }
                    span.status {
                        width: max-content;
                        border-radius: 8px;
                        font-size: 16px;
                        font-weight: 700;
                        line-height: 100%;
                        letter-spacing: 0;
                        display: flex;
                        &.active {
                            background-color: #87FFDF;
                            color: #24A483;
                        }
                        &.completed {
                            background-color: #FFDDDB;
                            color: #FD2517;
                        }
                    }
                }
            }
        }
    }
    @media (min-width: 768px) {
            main {
                height: 100vh;
                section.stake-panel {
                    width: 901px;
                    padding: 35px;
                    margin-top: 100px;
                    .stats {
                        flex-direction: row;
                    }

                    .history {
                        margin-top: 20px;
                        .metric {
                            flex-direction: row;
                            font-size: 18px;
                            font-weight: 400;
                            line-height: 100%;
                            letter-spacing: 0;
                            div {
                                span.field {
                                    display: none;
                                }
                                span.status {
                                    height: 43px;
                                    padding: 10px;
                                }
                            }
                        }
                    }
                }
            }
        }

        @media (max-width: 768px) {
            main {
                padding: 0px 30px;
                section.stake-panel {
                    width: 100%;
                    padding-bottom: 20px;
                    margin: 165px 0px 99px;
                    .stats {
                        flex-direction: column;
                        .staked {
                            width: 100%;
                        }
                        .other {
                            width: 100%;
                        }
                    }

                    .history {
                        width: 100%;
                        margin-top: 25px;
                        font-size: 15px;
                        font-weight: 400;
                        line-height: 100%;
                        letter-spacing: 0;
                        .fields {
                            width: 100%;
                            display: none;
                        }
                        .metric {
                            width: 100%;
                            flex-direction: column;
                            padding: 30px 20px;
                            gap: 20px;
                            div {
                                width: 100%;
                                display: flex;
                                justify-content: space-between;
                                align-items: center;
                                color: #333333;
                                span.status {
                                    height: 29px;
                                    padding: 5px 10px;
                                    color: #000000;
                                }
                            }
                        }
                    }
                }
            }
        }
</style>
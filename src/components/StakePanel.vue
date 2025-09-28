<script setup lang="ts">
import { onMounted, reactive } from 'vue';


interface DailyMetric {
  stakingDays: number;
  incomeDay: number;
  incomePeriod: number;
  expected: number;
  status: 'active' | 'pending' | 'completed';
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
        status: 'active'
    },
    {
        stakingDays: 17,
        incomeDay: 0.5,
        incomePeriod: 31.7,
        expected: 10,
        status: 'completed'
    },
    {
        stakingDays: 17,
        incomeDay: 0.5,
        incomePeriod: 31.7,
        expected: 10,
        status: 'active' 
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
    <section class="stake-panel">
        <div class="stats">
            <div class="staked">
                <p>Всього застекано</p>
                <h3>{{ userStats.staked }} BIN</h3>
                <p>Максимальний дохід по стекінгу 200%</p>
            </div>
            <div class="other">
                <div>
                    <p>Ребондіровано</p>
                    <span>{{ userStats.rebonded }}</span>
                </div>
                <div>
                    <p>Продано BIN</p>
                    <span>{{ userStats.binSolded }}</span>
                </div>
                <div>
                    <p>Заклеймено BIN</p>
                    <span>{{ userStats.binClaimed }}</span>
                </div>
            </div>
        </div>
        <div class="history">
            <ul class="metrics">
                <li class="fields">
                    <span>Дні стекінгу</span>
                    <span>Дохід за день</span>
                    <span>Дохід за період</span>
                    <span>Очікується</span>
                    <span>Статус</span>
                </li>
                <li class="metric" v-for="metric in dailyMetrics">
                    <span>{{ metric.stakingDays }}</span>
                    <span>{{ metric.incomeDay }}</span>
                    <span>{{ metric.incomePeriod }}</span>
                    <span>{{ metric.expected }}</span>
                    <span>{{ metric.status }}</span>
                </li>
            </ul>
        </div>
    </section>
</template>

<style scoped>
    section.stake-panel {
        width: 813px;
        height: 506;
        border-radius: 16px;
        border: 1px solid #E6E6E6;

        .stats {

        }

        .history {

        }
    }
</style>
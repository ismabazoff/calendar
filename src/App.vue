<template>
    <div class="month">
        <a href="#" @click="handlePrevMonthButtonClick"> &#10094; </a>
        {{ activeDate.format('MMMM').toUpperCase() }}
        <a href="#" @click="handleNextMonthButtonClick"> &#10095; </a>
    </div>
    <div class="weeks">
        <div class="week-day" v-for="weekDay in weekDays">
            {{ weekDay.toUpperCase() }}
        </div>
    </div>
    <div class="days">
        <template v-for="cell in cells">
            <div :class="{ active: cell.isToday, passed: cell.passedDays }">
                {{ cell.date.date() }}
                <Event
                    class="red"
                    date="16:00"
                    name="Presentation"
                    v-if="cell.date.date() == 2"
                />
                <Event
                    class="yellow"
                    date="18:00"
                    name="Семинар"
                    v-if="cell.date.date() == 2"
                />
                <Event
                    class="red"
                    date="16:00"
                    name="Presentation"
                    v-if="cell.date.date() == 26"
                />
                <Event
                    class="yellow"
                    date="18:00"
                    name="Семинар"
                    v-if="cell.date.date() == 26"
                />
                <Event
                    class="green"
                    date="18:00"
                    name="Коммуникационный дизайн среды"
                    v-if="cell.date.date() == 15"
                />
                <Event
                    class="green"
                    date="18:00"
                    name="Коммуникационный дизайн среды"
                    v-if="cell.date.date() == 24"
                />
            </div>
        </template>
    </div>
</template>

<script>
import Event from './components/Event.vue'
import moment from 'moment'
moment.locale('ru')

export default {
    name: 'App',
    components: {
        Event,
    },
    data() {
        return {
            weekDays: moment.weekdays(true),
            cells: [],
            today: null,
            activeDate: null,
        }
    },
    created() {
        const today = moment().startOf('day')
        this.today = today
        this.activeDate = today.clone()
    },
    methods: {
        handlePrevMonthButtonClick() {
            this.activeDate = this.activeDate.clone().subtract(1, 'month')
        },
        handleNextMonthButtonClick() {
            this.activeDate = this.activeDate.clone().add(1, 'month')
        },
    },
    watch: {
        activeDate() {
            const startDate = this.activeDate
                .clone()
                .startOf('month')
                .startOf('week')
                .startOf('day')
            const endDate = this.activeDate
                .clone()
                .endOf('month')
                .endOf('week')
                .startOf('day')
            const cells = []
            for (
                const date = startDate.clone();
                endDate.diff(date, 'days') >= 0;
                date.add(1, 'day')
            ) {
                cells.push({
                    date: date.clone(),
                    isToday:
                        date.format('YYYY-MM-DD') ===
                        this.today.format('YYYY-MM-DD'),
                    passedDays:
                        date.format('YYYY-MM-DD') <
                        this.today.format('YYYY-MM-DD'),
                })
            }
            this.cells = cells
        },
    },
}
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Kanit:wght@300;500&display=swap');

.active {
    color: #95bd99;
    border: 2px solid #9c9c9c;
    border-radius: 10px;
    font-family: 'Kanit', sans-serif;
    font-weight: bolder;
    text-align: right;
    padding-right: 6px;
}

.passed {
    color: #a4a4a4;
    background-color: #e6e6e6;
}

body {
    background-color: rgb(214, 213, 213);
}

div {
    font-family: Tahoma, Verdana, Segoe, sans-serif;
}
.title {
    padding: 30px;
    font-size: 3rem;
    text-align: center;
}
#app {
    width: 1200px;
    background-color: #fff;
    border-radius: 25px;
    padding: 0 25px 25px 25px;
}
.month {
    padding: 20px 20px 5px 0;
    font-size: 1.5rem;
    color: #373d7b;
    font-family: 'Kanit', sans-serif;
    font-weight: bolder;
}
.weeks {
    display: flex;
    flex-wrap: wrap;
}

.week-day {
    width: 100px;
    flex-grow: 1;
    margin-top: 5px;
    padding: 5px;
    text-align: right;
    font-family: 'Kanit', sans-serif;
    font-weight: bolder;
    &:nth-child(6),
    &:nth-child(7) {
        color: #a5a5a5;
    }
}

.days {
    display: grid;
    grid-template-columns: repeat(7, 1fr);
    grid-template-rows: 1fr;
    gap: 0px 0px;
    grid-template-areas: '. . . . . . .';
    div:not(.active) {
        border: 1px solid rgb(223, 223, 223);
        border-radius: 10px;
        height: 120px;
        width: 155px;
        margin: 1px;
        font-family: 'Kanit', sans-serif;
        font-weight: bolder;
        text-align: right;
        padding-right: 6px;
        &:nth-child(6),
        &:nth-child(7),
        &:nth-child(13),
        &:nth-child(14),
        &:nth-child(20),
        &:nth-child(21),
        &:nth-child(27),
        &:nth-child(28),
        &:nth-child(34),
        &:nth-child(35),
        &:nth-child(41),
        &:nth-child(42) {
            color: #a6aed1;
        }
        a {
            margin-right: 4px;
        }
    }
}

.day {
    height: 120px;
    width: 150px;
    flex: 1 0 auto;
    margin: 1px;
    border: 1px solid rgb(214, 213, 213);
    border-radius: 10px;
    text-align: right;
    padding-top: 10px;
    padding-right: 10px;
}
a {
    text-decoration: none;
    color: black;
    transition: all 0.5s ease-in-out;
}
a:hover {
    color: red;
}
</style>

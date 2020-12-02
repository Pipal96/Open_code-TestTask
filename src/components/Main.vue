<template>
    <div class="table table_frame">
        <header>
            <app-header @resultSearch="resultSearch($event)" @conditionMainField="conditionMainField"
                :columnOfTable="this.columnOfTable" :renderData="renderData" :forSearchData="forSearchData">
            </app-header>
        </header>
        <main>
            <section>

                <div class="wrapper table_border-bold">
                    <div class="row">
                        <div v-for="(column, index) in columnOfTable" :key="index"
                            class="tabel__border_bold js-main-row flex-center-center">
                            <span :value="column.nameColumn"
                                class="table__headline-field table__headline-field_size">{{ column.nameColumn }}</span>
                        </div>
                    </div>
                </div>

                <div id="renderDataBlock" class="wrapper table_border-lite" v-for="(data, index) in renderData"
                    :key="index">
                    <div class="row js-row-lite">
                        <div class="tabel__border_lite">
                            <span class="table__headline-field_size">{{data.business_name}}</span>
                        </div>
                        <div class="tabel__border_lite">
                            <span class="table__headline-field_size">{{data.business_location}}</span>
                        </div>
                        <div class="tabel__border_lite">
                            <span class="table__headline-field_size">{{data.business_city}}</span>
                        </div>
                        <div class="tabel__border_lite">
                            <span class="table__headline-field_size">{{data.business_phone_number}}</span>
                        </div>
                        <div class="tabel__border_lite">
                            <span class="table__headline-field_size">{{data.inspection_description}}</span>
                        </div>
                        <div class="tabel__border_lite">
                            <span class="table__headline-field_size">{{data.inspection_date}}</span>
                        </div>
                    </div>
                </div>
            </section>
        </main>
        <footer>
            <app-footer :renderData="this.renderData"></app-footer>
        </footer>
    </div>
</template>

<script>
    import Header from "./Header"
    import Footer from "./Footer"

    export default {
        components: {
            'app-header': Header,
            'app-footer': Footer,
        },
        data() {
            return {
                url: 'https://raw.githubusercontent.com/Pipal96/JSON_TEST/master/test.json',
                renderData: [],
                forSearchData: [],
                columnOfTable: [{
                        nameColumn: 'Название ресторана',
                        active: true,
                    },
                    {
                        nameColumn: 'Адрес ресторана',
                        active: true,
                    },
                    {
                        nameColumn: 'Город',
                        active: true,
                    },
                    {
                        nameColumn: 'Номер ресторана',
                        active: true,
                    },
                    {
                        nameColumn: 'Статус инспекции',
                        active: true,
                    },
                    {
                        nameColumn: 'Дата инспекции',
                        active: true,
                    },
                ]
            }
        },
        mounted() {
            this.getJSON()
        },
        methods: {
            async getJSON() {
                const getJSON = await fetch(this.url)
                this.renderData = await getJSON.json()
                this.forSearchData = this.renderData.slice()

            },
            conditionMainField(event, index) {
                document.querySelectorAll('.js-main-row').forEach(element => {
                    if (element.firstChild.getAttribute('value') == event) {
                        element.classList.toggle('hidden-elem')
                    }
                });

                document.querySelectorAll('.js-row-lite').forEach(element => {
                    element.children[index].classList.toggle('hidden-elem')
                });
            },
            resultSearch(event) {
                this.renderData = event
            },
        },
    }
</script>

<style scoped>
    .table {
        width: 100%;
        height: max(var(--height-tabel));
    }

    .table_frame {
        border: solid 1px var(--black-color);
        background-color: var(--white-color);
    }

    .wrapper {
        height: 82px;
        width: 100%;
    }

    .row {
        width: 100%;
        display: flex;
        justify-content: space-around;
        align-items: center;
        height: inherit;
    }

    .table_border-bold {
        border-top: solid 3px var(--black-color);
        border-bottom: solid 3px var(--black-color);
    }

    .table_border-lite {
        border-bottom: solid 1px var(--black-color);
    }

    .table__headline-field {
        width: 100%;
        height: 40px;
        display: flex;
        justify-content: center;
        align-items: center;
        padding: 0 20px;
        text-align: center;
    }

    .tabel__border_lite {
        width: 25%;
        height: 40px;
        display: flex;
        justify-content: center;
        align-items: center;
        padding: 0 20px;
        text-align: center;
    }

    .tabel__border_bold:not(:last-child) {
        border-right: solid 3px var(--black-color);
    }

    .tabel__border_lite:not(:last-child) {
        border-right: solid 1px var(--black-color);
    }

    .table__headline-field_size {
        font-size: 20px;
    }

    .flex-center-center {
        display: flex;
        justify-content: center;
        align-items: center;
        width: 100%;
    }

    .hidden-elem {
        display: none;
    }
</style>
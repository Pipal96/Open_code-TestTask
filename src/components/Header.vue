<template>
    <div class="wrapper">
        <div class="row">
            <h1>Инспекция по ресторанам</h1>
            <div class="dropdown">
                <div @click="showDropdownList" aria-label="Кнопка редактирования таблицы"
                    class="dropdown__list dropdown__list_condition" :class="{ 'active-button': conditonButton}">
                    Редактировать таблицу
                </div>

                <ul v-if="this.seeDropdown" class="dropdown__items">
                    <li @click="switchingVisibility(index, $event)" v-for="(item, index) in columnOfTable" :key="index"
                        :value="item.nameColumn" class="dropdown__item">

                        <app-done-svg-icon v-if="item.active" class="svg-icon_padding"></app-done-svg-icon>
                        <app-close-svg-icon v-else class="svg-icon_padding"></app-close-svg-icon>

                        {{item.nameColumn}}
                    </li>

                </ul>
            </div>
            <div class="search">
                <form @submit.prevent="searchElem" action="#">
                    <fieldset>
                        <legend hidden>Поле ввода для поиска по полям таблицы</legend>
                        <label hidden for="search">Поиск по полям таблицы</label>
                        <input v-model.trim="valueFieldSearch" class="search-field" type="text" name="search-field"
                            id="search" placeholder="Поиск по полям таблицы">
                    </fieldset>
                </form>
            </div>
        </div>
    </div>
</template>

<script>
    import DoneSvg from "./DoneSvg"
    import CloseSvg from "./CloseSvg"

    export default {
        components: {
            'app-done-svg-icon': DoneSvg,
            'app-close-svg-icon': CloseSvg,
        },
        data() {
            return {
                resultSearch: [],
                seeDropdown: false,
                conditonButton: false,
                conditionColumnTable: true,
                valueFieldSearch: '',
                textSearch: '',
            }
        },
        props: ['columnOfTable', 'renderData', 'forSearchData'],

        methods: {
            showDropdownList() {
                this.seeDropdown = !this.seeDropdown
                this.activeButton()
            },
            activeButton() {
                this.conditonButton = !this.conditonButton
            },
            switchingVisibility(index, event) {
                this.conditionColumnTable = !this.conditionColumnTable
                this.columnOfTable[index].active = !this.columnOfTable[index].active

                this.$emit('conditionMainField', event.target.getAttribute("value"), index)
            },
            searchElem() {
                this.textSearch = this.valueFieldSearch
                this.valueFieldSearch = ''

                this.resultSearch = []

                this.forSearchData.forEach(object => {
                    for (const props in object) {
                        if (object[props] == this.textSearch) {
                            this.resultSearch.push(object)
                        }
                    }
                });
                this.$emit('resultSearch', this.resultSearch)
            }
        },
    }
</script>

<style scoped>
    .wrapper {
        height: 82px;
        width: 100%;
    }

    h1 {
        font-size: 24px;
    }

    .row {
        display: flex;
        justify-content: space-around;
        align-items: center;
        height: inherit;
    }

    .dropdown {
        position: relative;
    }

    .dropdown__list_condition {
        width: 335px;
        height: 46px;
        font-size: 18px;

        display: flex;
        justify-content: center;
        align-items: center;
        border: solid 1px var(--black-color);
        cursor: pointer;
        transition: 0.2s;
        box-sizing: border-box;
    }

    .dropdown__list_condition:hover {
        background-color: var(--background-dropdown-button);
        transition: 0.2s;
    }

    .dropdown__items {
        padding: 0px;
        margin: 0px;
        position: absolute;
        list-style: none;
        width: var(--width-dropdown-item);
        height: calc(var(--height-dropdown-item)*7);
        top: 100%;
    }

    .dropdown__item {
        width: var(--width-dropdown-item);
        height: var(--height-dropdown-item);
        background-color: var(--white-color);
        box-sizing: border-box;
        border-left: solid 1px var(--black-color);
        border-right: solid 1px var(--black-color);
        border-bottom: solid 1px var(--black-color);
        cursor: pointer;
        display: flex;
        align-items: center;
    }

    .dropdown__item:hover {
        background-color: var(--background-dropdown-button);
    }

    .active-button {
        background-color: var(--background-dropdown-button);
    }

    .svg-icon_padding {
        padding: 0 7px;
    }

    .search-field {
        width: 429px;
        height: 46px;
        border: solid 1px var(--border-color);
        padding: 6px 0px 6px 16px;
        box-sizing: border-box;
    }
</style>
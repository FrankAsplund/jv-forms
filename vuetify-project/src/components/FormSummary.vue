<template>
    <v-form>
        <div class="text-h3">Summering</div>
        <div class="line-divider"></div>

        <div class="summary-info">
            <div class="text-body-2">
                Här har du möjlighet att granska, gå tillbaka och ändra. <br />
                Du kan hoppa till valfritt avsnitt genom att klicka på önskad sida i listan ovan.
                Ändra uppgift och klicka sedan på denna sida i listan igen
            </div>
        </div>

        <div class="flex-container">
            <div class="flex-child">
                <div class="box-title">Grunduppgifter</div>
                <v-table density="compact">
                    <thead>
                        <tr>
                            <th class="text-left">Förnamn</th>
                            <th class="text-right"> {{ formData.firstname }}</th>
                        </tr>
                        <tr>
                            <th class="text-left">Efternamn</th>
                            <th class="text-right"> {{ formData.lastname }}</th>
                        </tr>
                        <tr>
                            <th class="text-left">Personnummer</th>
                            <th class="text-right"> {{ formData.ssn }}</th>
                        </tr>
                        <tr>
                            <th class="text-left">Epost address</th>
                            <th class="text-right"> {{ formData.email }}</th>
                        </tr>
                        <tr>
                            <th class="text-left">Telefonnummer</th>
                            <th class="text-right">{{ formData.phoneNumber }}</th>
                        </tr>
                        <tr>
                            <th class="text-left">Jag söker som</th>
                            <th class="text-right">{{ formData.apply }}</th>
                        </tr>
                        <tr>
                            <th class="text-left">Länsbokstav</th>
                            <th class="text-right">{{ formData.applyCounty.name }}</th>
                        </tr>
                        <tr>
                            <th class="text-left">Länsnummer</th>
                            <th class="text-right">{{ formData.applyNumber }}</th>
                        </tr>
                    </thead>
                </v-table>
                <div class="summary-btn">
                    <v-btn color="success">Ändra uppgifter</v-btn>
                </div>
            </div>


            <div class="flex-child">
                <div class="box-title">Ansökan</div>
                <div class="text-caption">

                </div>
                <v-table density="compact">
                    <thead>
                        <tr>
                            <th class="text-left">Antal kalkoner över 24 veckor i din besättning:</th>
                            <th class="text-right">{{ formDataApply.averageHensOlderThan20WeeksThisYear }}</th>
                        </tr>
                        <tr>
                            <th class="text-left">Antal slaktkycklingar i normal uppfödningsomgång:</th>
                            <th class="text-right">{{ formDataApply.averageChickensSlaughteredThisYear }}</th>
                        </tr>
                        <tr>
                            <th class="text-left">Antal kalkonkyckling för äggproduktion:</th>
                            <th class="text-right">{{ formDataApply.averageEggProducingChickensThisYear }}</th>
                        </tr>
                        <tr>
                            <th class="text-left">Total summa:</th>
                            <th class="text-right">Nej</th>
                        </tr>
                        <tr>
                            <th class="text-left">Jag söker krisstöd för min fjäderfäproduktion</th>
                            <th class="text-right">{{ formDataApply.productionType }}</th>
                        </tr>
                    </thead>
                </v-table>
                <div class="summary-btn">
                    <v-btn color="success">Ändra uppgifter</v-btn>
                </div>
            </div>
        </div>

        <v-container class="summaryConfirmContainer" fluid>
            <div class="text-subtitle-1">Godkännande och försäkran</div>
            <v-checkbox v-model="summaryCheckbox" color="success">
                <template v-slot:label>
                    <div>
                        <div class="text-body-2">Härmed ansöker jag om krisstödet 2023</div>
                        <v-list>Jag intygar att: <br />
                            <v-list-item prepend-icon="mdi-circle-small">Jag är införstådd med och uppfyller de villkor
                                som
                                finns för att få ta del av
                                stödet.</v-list-item>
                            <v-list-item prepend-icon="mdi-circle-small">Ansökan inte gäller ett företag i ekonomiska
                                svårigheter enligt art. 2.14 i
                                förordningen
                                (EU) nr
                                702/2014</v-list-item>
                        </v-list>
                    </div>
                </template>
            </v-checkbox>
            <div class="send-btn" v-if="summaryCheckbox">
                <v-btn @click="submit()" color="success">Skicka in</v-btn>
            </div>
        </v-container>
    </v-form>
</template>

<script setup>
import { ref } from 'vue';

const props = defineProps({
    formData: {
        type: Object,
    },
    formDataApply: {
        type: Object,
    },
});

const summaryCheckbox = ref(false);

const emit = defineEmits(['submit-all'])

const submit = () => {
    emit("submit-all");
}

</script>

<style scoped>
.summary-btn {
    text-align: center;
    padding: 10px;
}

.summaryConfirmContainer {
    margin: auto;
    width: 70%;
    box-shadow: rgba(60, 64, 67, 0.3) 0px 1px 2px 0px, rgba(60, 64, 67, 0.15) 0px 1px 3px 1px;
    padding: 10px;
    margin-bottom: 0.5rem;
}

.flex-container {
    display: flex;
    margin-bottom: 2rem;
    width: 100%;
}

.flex-child {
    flex: 1;
    box-shadow: rgba(60, 64, 67, 0.3) 0px 1px 2px 0px, rgba(60, 64, 67, 0.15) 0px 1px 3px 1px;
}

.flex-child:first-child {
    margin-right: 20px;
    box-shadow: rgba(60, 64, 67, 0.3) 0px 1px 2px 0px, rgba(60, 64, 67, 0.15) 0px 1px 3px 1px;
}

.box-title {
    font-size: 16px;
    font-weight: bold;
}

.apply-info {
    padding-bottom: 1.1rem;
}

.h1-summary {
    margin-top: 1.5rem;
}

.line-divider {
    margin-top: 1.5rem;
    margin-bottom: 0.5rem;
    border-bottom: 2px solid rgb(156, 207, 111)
}

.summary-info {
    margin-bottom: 1.5rem;
}
</style>
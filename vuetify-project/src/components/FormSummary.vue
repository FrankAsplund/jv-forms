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
                            <th class="text-right">Daniel</th>
                        </tr>
                        <tr>
                            <th class="text-left">Efternamn</th>
                            <th class="text-right">Bladh Stenberg</th>
                        </tr>
                        <tr>
                            <th class="text-left">Personnummer</th>
                            <th class="text-right">1992-10-18-XXXX</th>
                        </tr>
                        <tr>
                            <th class="text-left">Jag ansöker som:</th>
                            <th class="text-right">Privatperson</th>
                        </tr>
                        <tr>
                            <th class="text-left">Länsbokstav</th>
                            <th class="text-right">AB-Stockholm</th>
                        </tr>
                        <tr>
                            <th class="text-left">Nummer</th>
                            <th class="text-right">XXXXXX</th>
                        </tr>
                        <tr>
                            <th class="text-left">E-post</th>
                            <th class="text-right">daniel@onify.co</th>
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
                    Produktion som jag söker krisstöd för. <br />
                    Om du har sökt gårdsstöd eller nötkreaturstöd i SAM Internet 2019 så kommer Jordbruksverket att
                    basera
                    ditt krisstöd på de uppgifter som du
                    angett i din SAM-ansökan.
                </div>
                <v-table density="compact">
                    <thead>
                        <tr>
                            <th class="text-left">Om jag fick gårdsstöd 2018</th>
                            <th class="text-right">Ja</th>
                        </tr>
                        <tr>
                            <th class="text-left">Om jag fick nötkreatursstöd 2018</th>
                            <th class="text-right">Ja</th>
                        </tr>
                        <tr>
                            <th class="text-left">Jag söker krisstöd för min får- och getproduktion</th>
                            <th class="text-right">Ja</th>
                        </tr>
                        <tr>
                            <th class="text-left">Jag söker krisstöd för min grisproduktion</th>
                            <th class="text-right">Nej</th>
                        </tr>
                        <tr>
                            <th class="text-left">Jag söker krisstöd för min fjäderfäproduktion</th>
                            <th class="text-right">Nej</th>
                        </tr>
                    </thead>
                </v-table>
                <div class="summary-btn">
                    <v-btn color="success">Ändra uppgifter</v-btn>
                </div>
            </div>
        </div>

        <v-container class="summaryConfirm" fluid>
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
            <div class="send-btn">
                <v-btn v-bind:disabled="summaryCheckbox === false" color="success">
                    Skicka in
                </v-btn>
            </div>
        </v-container>
    </v-form>
</template>

<script>
export default {
    data() {
        return {
            summaryCheckbox: false,
        }
    }
}
</script>

<style scoped>
.summary-btn {
    text-align: center;
    padding: 10px;
}

.summaryConfirm {
    margin: auto;
    width: 50%;
    box-shadow: rgba(60, 64, 67, 0.3) 0px 1px 2px 0px, rgba(60, 64, 67, 0.15) 0px 1px 3px 1px;
    padding: 10px;
    margin-bottom: 0.5rem;
}

.send-btn {
    text-align: center;
}

.flex-container {
    display: flex;
    margin-bottom: 2rem;
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
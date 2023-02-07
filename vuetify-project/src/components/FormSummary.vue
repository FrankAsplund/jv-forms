<template>

    <h1 class="h1-summary">Summering</h1>
    <div class="line-divider"></div>

    <div class="summary-info">
        <p>
            Här har du möjlighet att granska, gå tillbaka och ändra. <br />
            Du kan hoppa till valfritt avsnitt genom att klicka på önskad sida i listan ovan.
            Ändra uppgift och klicka sedan på denna sida i listan igen
        </p>
    </div>

    <div class="flex-container">
        <div class="flex-child">
            <div class="box-title">Grunduppgifter</div>
            <v-text-field prepend-inner-icon="mdi-account-box" type="text" label="Personnummer" />
            <v-text-field prepend-inner-icon="mdi-alpha-a-box" type="text" label="Förnamn" />
            <v-text-field prepend-inner-icon="mdi-alpha-a-box" type="text" label="Efternamn" />
            <v-text-field prepend-inner-icon="mdi-form-select" label="Du ansöker som:" />
            <v-text-field prepend-inner-icon="mdi-form-select" type="text" label="Länsbokstav" />
            <v-text-field prepend-inner-icon="mdi-pound-box" type="text" label="Nummer" />
            <v-text-field prepend-inner-icon="mdi-account-box" type="email" label="E-post" />
            <v-btn class="summary-btn" color="success">Ändra uppgifter</v-btn>
        </div>

        <div class="flex-child">
            <div class="box-title">Ansökan</div>
            <p class="apply-info">
                Produktion som jag söker krisstöd för. <br />
                Om du har sökt gårdsstöd eller nötkreaturstöd i SAM Internet 2019 så kommer Jordbruksverket att basera
                ditt krisstöd på de uppgifter som du
                angett i din SAM-ansökan.
            </p>
            <v-text-field label="Om jag fick gårdsstöd 2018" suffix="Ja" />
            <v-text-field label="Om jag fick nötkreatursstöd 2018" suffix="Ja" />
            <v-text-field label="Jag söker krisstöd för min får- och getproduktion" suffix="Ja" />
            <v-text-field label="Jag söker krisstöd för min fjäderfäproduktion" suffix="Nej" />
            <v-text-field value="Jag söker krisstöd för min grisproduktion" suffix="Nej" />
            <v-text-field value="Jag söker krisstöd för min grisproduktion" suffix="Nej" />
            <v-btn class="summary-btn" color="success">Ändra uppgifter</v-btn>
        </div>
    </div>

    <v-container class="summaryConfirm" fluid>
        <h3>Godkännande och försäkran</h3>
        <v-checkbox v-model="summaryCheckbox" color="success">
            <template v-slot:label>
                <div>
                    <p>Härmed ansöker jag om krisstödet 2023</p>
                    <p>Jag intygar att: <br />
                        <li>Jag är införstådd med och uppfyller de villkor som finns för att få ta del av stödet.</li>
                        <li>Ansökan inte gäller ett företag i ekonomiska svårigheter enligt art. 2.14 i förordningen
                            (EU) nr
                            702/2014</li>
                    </p>
                </div>
            </template>
        </v-checkbox>
        <div class="send-btn">
            <v-btn class="send-btn" v-bind:disabled="summaryCheckbox === false" color="success">
                Skicka in
            </v-btn>
        </div>
    </v-container>
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
    border-bottom: 2px solid brown
}

.summary-info {
    margin-bottom: 1.5rem;
}
</style>
<template>
    <div>
        <AppSubheader></AppSubheader>
        <section class="section section-lg pt-lg-0 mt-5">
            <div class="container">
                <div class="row mb-lg">
                    <div class="col-lg-12">
                        <h2>hfg.design Support</h2>
                    </div>
                    <div class="col-lg-8 ml-auto mt-4">
                        <h4>Login funktioniert nicht? 😕</h4>
                        <h4>Emails kommen nicht an? 🤔</h4>
                        <h4>Webcam liefert kein Bild? 🤯</h4>
                        <p
                            class="mt-4"
                        >Kann passieren. Nicht verzweifeln, wir kriegen das schon geregelt.</p>
                        <br />
                        <p>
                            <strong>Bevor du dich aber bei unserem Support meldest, gehe bitte nochmal durch diese Schritte:</strong>
                        </p>
                        <ul class="decimal">
                            <li class="decimal">Google it.</li>
                            <li>Schau nochmal die FAQs an, ob das Thema dort erklärt wird. Oft werden dort auch externe Videos verlinkt, die dir unter Umständen weiterhelfen.</li>
                            <li>Falls das nichts nützt, frag' deinen Buddy. Jeder Jahrgang hat einen studentischen Ansprechpartner für Tutorials, vielleicht wissen die, wie man dein Problem löst.</li>
                            <li>Nützt das alles nichts, gibt es auch Ansprechpartner an der HfG. Siehe unten, wen du wofür fragen kannst.</li>
                        </ul>
                    </div>
                </div>

                <div class="row mb-lg">
                    <div class="col-lg-4">
                        <h2>Technischer Support</h2>
                    </div>
                    <div class="col-lg-8">
                        <p>
                            <strong>Wir haben euch ein Team für technische Fragen bereitgestellt. Hier unterscheiden wir zwischen dem User- & Hardware-Support.</strong>
                        </p>
                        <br />
                        <h4>User-Support:</h4>
                        <p class="mb-0">
                            Wenn ihr Probleme mit den Software-Tools habt, sind wir zur Stelle.
                            <br />
                            <br />
                        </p>
                        <strong>Wir beantworten Fragen wie:</strong>
                        <ul>
                            <li>Wie melde ich mich mit meinem hfg.design Konto bei Tools wie Slack oder Zoom an?</li>
                            <li>Wie finde ich meinen Stundenplan?</li>
                            <li>Wie finde ich den Slack-Channel zu meiner Vorlesung?</li>
                        </ul>
                        <br />
                        <h4>Hardware-Support:</h4>
                        <p class="mb-0">
                            Sollte Ihr Probleme mit eurer Hardware haben. Eure Webcam, Mikrofon, etc. funktionieren nicht, dann seid ihr hier genau richtig.
                            <br />
                            <br />
                        </p>
                        <strong>Wir beantworten Fragen wie:</strong>
                        <ul>
                            <li>Warum funktioniert meine Webcam nicht?</li>
                            <li>Warum ist mein Internet zu Hause nicht schnell genug?</li>
                            <li>Welche Hardware wird generell empfohlen?</li>
                            <li>Welche Hardware kann ich mir von der HfG ausleihen?</li>
                        </ul>
                    </div>
                </div>

                <ContactCard :passContactCardContent="passTechSupport" />

                <div class="row mb-lg mt-5">
                    <div class="col-lg-4">
                        <h2>Organisatorischer Support</h2>
                        <h2 class="font-weight-normal">für Dozenten und Mitarbeiter</h2>
                    </div>
                    <div class="col-lg-8">
                        <p>
                            <strong>Wir beantworten euch organisatorische Fragen rund um die Online-Lehre und das Portal hfg.design, wie z.B.:</strong>
                        </p>
                        <ul>
                            <li>Wie verschiebe ich einen Termin in meinem Stundenplan?</li>
                            <li>Wie finde ich die Details zu meiner Vorlesung?</li>
                            <li>Wie kontaktiere ich meine Studenten in Slack?</li>
                        </ul>
                        <p class="mt-5"><strong>Kontaktiert bitte den Akademischen Mitarbeiter eures Studiengangs direkt per E-Mail. Wenn das nicht klappt oder es dringend ist, ist Julia auch telefonisch erreichbar.</strong></p>
                    </div>
                </div>

                <ContactCard :passContactCardContent="passOrgaSupport" />
            </div>
        </section>
    </div>
</template>

<script>
import ContactCard from "../components/Support/ContactCard";
import Modal from "../components/Modal";
import AppSubheader from "@/layout/AppSubheader";

export default {
    name: "home",
    components: {
        AppSubheader,
        ContactCard,
        Modal
    },

    data: function() {
        return {
            passTechSupport: [
                {
                    supportTeam: "User-Support",
                    name: "",
                    email: "support@hfg.design",
                    slack: "C011RA4JY3C",
                    tel: "07171 / 9782912",
                    option: "",
                    reach1: "9:00 – 17:00 Uhr",
                    imgPath: "img/support/team/user-support-1.jpg",
                    question:
                        "Warum funktioniert meine @hfg.design Anmeldung nicht?"
                },
                {
                    supportTeam: "Hardware-Support",
                    name: "Aiko Scheuvens",
                    email: "support@hfg.design",
                    slack: "C011RA4JY3C",
                    tel: "07171 / 602623 ",
                    option: "",
                    reach1: "9:00 – 17:00 Uhr",
                    imgPath: "img/support/team/tech-support.jpg",
                    question: "Hilfe, meine Vorlesung beginnt, meine Webcam funktioniert nicht!?"
                }
            ],
            passOrgaSupport: [
                {
                    supportTeam: "Orga-Support",
                    name: "Julia Wittich",
                    email: "am-ma@hfg.design",
                    slack: "C011RA4JY3C",
                    tel: "07171 / 9782916",
                    option: "(bitte nur Dozenten, Profs oder Mitarbeiter)",
                    reach1: "9:00 – 17:00 Uhr",
                    imgPath: "img/support/team/am-support.jpg",
                    question: "Hilfe, wie erreiche ich meine Studenten?"
                }
            ],
            feedbackMessage: "",
            feedbackWasSent: false,
            feedbackConfirmation: "Sende Feedback...",
            errorModal: false
        };
    },
    methods: {
        sendFeedback: function() {
            this.feedbackWasSent = true;
            this.$http
                .post(
                    "https://76i3an3137.execute-api.eu-central-1.amazonaws.com/prod/slackbridge/feedback",
                    JSON.stringify({
                        text: this.feedbackMessage
                    }),
                    {
                        headers: {
                            Accept: "application/json, text/plain, */*"
                        }
                    }
                )
                .then(result => {
                    this.feedbackConfirmation =
                        "Wir haben dein Feedback erhalten - vielen Dank!";
                })
                .catch(error => {
                    // handle error
                    this.feedbackConfirmation =
                        "Leider ist etwas beim Versenden deines Feedbacks schief gegangen, bitte wende dich an einen der oben genannten Supportkontakte!";
                    this.errorModal = true;
                    this.feedbackWasSent = false;
                    console.log(error);
                });
        }
    }
};
</script>

<style scoped>
ul li {
    margin-left: -22px;
    font-size: 1.125rem;
}
ul.decimal li {
    list-style-type: decimal;
    margin-left: -22px;
    font-size: 1.125rem;
}
strong {
    font-size: 1.125rem;
}
</style>

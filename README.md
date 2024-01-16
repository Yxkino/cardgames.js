const PromptSync = require('prompt-sync');
const prompt = PromptSync();

console.log("Bienvenue au jeu de cartes !");
const pseudo = prompt("Entrez votre pseudo : ");
console.log("Bonjour " + pseudo + "! Le jeu va commencer.");
startGame();

function startGame() {
    let playerCards = ['Eau', 'Feu', 'Plante'];
    let robotCards = ['Eau', 'Feu', 'Plante'];

    let playerScore = 0;
    let robotScore = 0;

    for (let i = 0; i < 3; i++) {
        console.log("Manche " + (i + 1));

        console.log("0: Eau, 1: Feu, 2: Plante");
        let playerChoice01 = prompt("Choisir votre carte : ");
        let playerChoice = playerCards[playerChoice01];
        let robotChoice = getRobotChoice(robotCards);

        console.log("Vous avez choisi " + playerChoice);
        console.log("Le robot a choisi " + robotChoice);

        let result = determineResult(playerChoice, robotChoice);
        if (result === 'Victoire') {
            playerScore++;
        } else if (result === 'Défaite') {
            robotScore++;
        }
    }

    console.log("Résultat final : Vous : " + playerScore + " - Robot : " + robotScore);

    if (playerScore === robotScore) {
        console.log("Égalité !");
        const rejouer = prompt("Voulez-vous rejouer ? (oui/non) : ");
        if (rejouer.toLowerCase() === 'oui') {
            console.log("Nouvelle partie !");
            startGame();
        } else {
            console.log("Fin du jeu.");
        }
    } else {
        console.log("Le gagnant est : " + (playerScore > robotScore ? 'Vous' : 'Le Robot'));
    }
}


function getRobotChoice(robotCards) {
    return robotCards[Math.floor(Math.random() * robotCards.length)];
}

function determineResult(playerChoice, robotChoice) {
    if ((playerChoice === 'Eau' && robotChoice === 'Feu') ||
        (playerChoice === 'Feu' && robotChoice === 'Plante') ||
        (playerChoice === 'Plante' && robotChoice === 'Eau')) {
        return 'Victoire';
    } else if (playerChoice === robotChoice) {
        return 'Égalité';
    } else {
        return 'Défaite';
    }
}

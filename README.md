# dapp-contract-created-code
<!DOCTYPE html>
<html lang="en">
  <head>
    <style>
        body {
          text-align: center;
          font-family: Arial, Helvetica, sans-serif;
        }
      
        div {
          width: 20%;
          margin: 0 auto;
          display: flex;
          flex-direction: column;
        }
      
        button {
          width: 100%;
          margin: 10px 0px 5px 0px;
        }
      </style>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>LearnWeb3 First dApp</title>
  </head>
  <body>
  <!-- We will add more code here -->
  </body>
</html>

<body>
    <div>
      <h1>This is my dApp!</h1>
      <p>Here we can set or get the mood:</p>
      <label for="mood">Input Mood:</label> <br />
      <input type="text" id="mood" />
  
      <button onclick="getMood()">Get Mood</button>
      <button onclick="setMood()">Set Mood</button>
      <p id="showMood"></p>
    </div>
</body>

<script
  src="https://cdn.ethers.io/lib/ethers-5.7.2.umd.min.js"
  type="application/javascript"
></script>

<script>
        const MoodContractAddress = "0xE955295a554FA766F6c665C2c4E55138560Ccf51";
        const MoodContractABI = [
	{
		"inputs": [],
		"name": "getMood",
		"outputs": [
			{
				"internalType": "string",
				"name": "",
				"type": "string"
			}
		],
		"stateMutability": "view",
		"type": "function"
	},
	{
		"inputs": [
			{
				"internalType": "string",
				"name": "_mood",
				"type": "string"
			}
		],
		"name": "setMood",
		"outputs": [],
		"stateMutability": "nonpayable",
		"type": "function"
	}
]

const provider = new ethers.providers.Web3Provider(window.ethereum, "sepolia"); 

provider.send("eth_requestAccounts", []).then(() => {
    provider.listAccounts().then((accounts) => {
        signer = provider.getSigner(accounts[0]);
        MoodContract = new ethers.Contract(
            MoodContractAddress,
            MoodContractABI,
            signer
        );
    });
});


async function getMood() {
    const mood = await MoodContract.getMood();
    document.getElementById("showMood").innerText = "Your Mood: "+ mood;
    console.log(mood);

}

async function setMood() {
    const mood = document.getElementById("mood");
    if(mood.value==""){
        mood.placeholder="Enter Your Mood";
        mood.focus();
    }else{
        await MoodContract.setMood(mood.value);
    }
}
</script>

</html>

<script>
// @ts-nocheck

  let isDisabled = false

  let userName = ""
  let dayValue = 0
  let monthValue = null
  let yearBorn = null
  let today = new Date()
  let year = today.getFullYear()
  let years =[]
  let month = today.getMonth() + 1
  let day = today.getDate()
  let age = null

  //Objekt som representerer interessene og veridene hver interesse med følger
  let rows = [
    {
      id: 1,
      text: 'Matlaging og baking',
      options: ['Foodora', 'Grandis', 'Må jo ha mat', 'Liker digg mat', 'Hjemmelaget er best']
    },
    {
      id: 2,
      text: 'Sport og trening',
      options: ['Elsker soffan', 'Har medlemskap', 'Trener jevnlig', 'Trener ofte', 'Jeg skal bli proff']
    },
    {
      id: 3,
      text: 'Friluftsliv',
      options: ['Voi til bussen', 'Liker meg inne', 'Har turutstyr', 'Liker meg ute', 'Fjellgeit']
    },
    {
      id: 4,
      text: 'Film og tv serier',
      options: ['Leser heller boka', 'Blir fort lei', 'Sprøs hva?', 'Har sett den', 'Yess! 15 sesonger']
    },
    {
      id: 5,
      text: 'Gaming',
      options: ['Nei takk', 'Kontroller er vansklig', 'Gamer av og til', 'Nerd', 'Hva er gress?']
    },
    {
      id: 6,
      text: 'Programering',
      options: ['Hva er det?', 'Hater det', 'Midt på 3', 'Gjør det på skolen', 'Høy interesse']
    },
    {
      id: 7,
      text: 'Vitenskap og teknologi ',
      options: ['Jorda er flat', 'Lite interesert', 'Midt på 3', 'Ganske høy interesse', 'Lager bombe i garasje']
    },
    {
      id: 8,
      text: 'Historie, kultur og littratur',
      options: ['Er ikke Islam et land?', 'Kjedelig', 'Gøy av og til', 'THE ROMAN EMPIRE!', 'Høyt interisert']
    },
    {
      id: 9,
      text: 'Bygg og snekring',
      options: ['IKKE gi meg saks!', 'Spiker eller skure?', 'Pappas lille hjelper', 'Jeg fikser selv', 'Jeg går bygg']
    },
    {
      id: 10,
      text: 'Kunst, maling og arkitektur',
      options: ['NEI TAKK', 'OK', 'Farger er gøy', 'Kan tegne', 'Har malingsflekker overalt']
    },
    {
      id: 11,
      text: 'Klær og mote',
      options: ['Bryr meg ikke', 'Bruker forskjellige sokker', 'Vil se bra ut', 'Ser bra ut', 'Trendfølger']
    },
    {
      id: 12,
      text: 'Religion',
      options: ['Ikke troende', 'Liker fordelene', 'Litt religiøs', 'Chiller med Gud', 'Fult troende']
    },
  ];

  
  let selectedOption = {};
  //mine svar på interesser 
  const mySelectedOption = [3,4,2,4,4,5,4,3,2,1,4,2]
  let selectedOptionAtAll = false

  let WhouldYouRatherUserAnswers = {}
  //mine svar på Would you rather
  const WYRMyAnswers = [1,2,2,2,2,1,1,1,1,2]
  let qNumber = 0

  const WhouldYouRatherQ = ['Vil du ha hvilken som helst super kraft', 'Være den rikeste personen i verden', 'Snakke med dyr', 'Snakke alle språk i verden', 'Gå på knust glass', 'Falle på en kaktus', 'Kunne ta form av hvilket som helst dyr', 'Kunne ta form til hvilket som helst menneske', 'Bli født blind', 'Bli født døv', 'Hund', 'Katt', 'Være i fengsel i 5 år', 'Være i koma i 10 år', 'Vite alt', 'Ha alt', 'Utforske verdensrommet', 'Utforske det dype hav', 'Vil du heller alltid være 10 minutter for sent til alt','Alltid være 20 minutter for tidlig']
  let WYRQNumber = 1

  let endScoreOfInterest = null
  let endScoreOfWYR = null
  let totalScore = null


  let scoreVisible = false
  let WYRVisible = false

  //plaserer inn verdiene 
  rows.forEach(row => {
    selectedOption[row.id] = row.options[0];
  });

  //Starter alle veridene med null istden for unifiend
  rows.forEach(row => {
    selectedOption[row.id] = null;
  });


  //putter in 100 år inn i valg av år
  for (let i = year; i >= year - 100; i--){
    years.push(i)
  }

  //setter veriden fra den valgte radio knappen in i et array for valgte options av brukern
  function handleRadioChange(event){
    let rowId = event.target.name;
    let selectedValue = event.target.value;
    selectedOptionAtAll = true
    selectedOption[rowId] = selectedValue;
  }
  
  function changedName(){
    let AgeDiv = document.querySelector('.AgeDefiner');
    let AgeText = document.querySelector('#AgeText');

    AgeDiv.style.filter = 'blur(' + 0 + ')';
    AgeText.style.filter = 'blur(' + 0 + ')';
  }

  function CheckAgeComplet(){
    if (yearBorn !== null && monthValue !== null && dayValue !== 0){
      let InterestDiv = document.querySelector('#interestsContainer');
      let NextButton = document.querySelector('#NextSectionButton');
      NextButton.style.filter = 'blur(' + 0 + ')';
      InterestDiv.style.filter = 'blur(' + 0 + ')';
    }
  }

  function dayChange(){
    let DayCounter = document.getElementById("DayCounter");
    DayCounter.style.visibility = "visible"
    if (monthValue !== null && yearBorn !== null){
      age = year - yearBorn
      if (monthValue > month){
        age = age - 1
        console.log(age)
      }
      if (monthValue == month){
        if (dayValue > day){
          age = age - 1
        }
      }
    }
    CheckAgeComplet()
  }

  function monthChange(){
    let DayCounter = document.getElementById("DayCounter");
    DayCounter.style.visibility = "visible"
    const dayElement = document.getElementById("daySlider");
    //Setter in riktig antall dager for hver månåed
    if (monthValue == 1 || monthValue == 3 || monthValue == 5 || monthValue == 7 || monthValue == 8 || monthValue == 10 || monthValue == 12){
      // @ts-ignore
      dayElement.max = 31
    }
    else if (monthValue == 4 || monthValue == 6 || monthValue == 9 || monthValue == 11){
      // @ts-ignore
      dayElement.max = 30
      if (dayValue >30){
        dayValue = 30
      }
    }
    else{
      // @ts-ignore
      dayElement.max = 28
      if (dayValue >28){
        dayValue = 28
      }
    }
    CheckAgeComplet()
  }
  
  function yearChange(){
    let DayCounter = document.getElementById("DayCounter");
    DayCounter.style.visibility = "visible"
    CheckAgeComplet()
  }


  //setter in brukerns svar fra WYR
  function nextWYR(){
    qNumber ++
    let Button1 = document.getElementById("WYRButton1");
    let Button2 = document.getElementById("WYRButton2");
    Button1.innerHTML = WhouldYouRatherQ[(qNumber*2)];
    Button2.innerHTML = WhouldYouRatherQ[(qNumber*2) +1];
  }

  function WYRAnswer1(){
    WhouldYouRatherUserAnswers[qNumber] = 1
    WYRQNumber = WYRQNumber + 1
    if (WYRQNumber > 10){
      getScore()
    }
    else{
      nextWYR()
    }
    
  }

  function WYRAnswer2(){
    WhouldYouRatherUserAnswers[qNumber] = 2 
    WYRQNumber = WYRQNumber + 1
    if (WYRQNumber > 10){
      getScore()
    }
    else{
      nextWYR()
    }
  }


  function NextSectionFun(){
    let checkedInterest = 0
    if (userName !== ""){
      if (age !== null){
        for (let b = 0; b < 13; b++){
          if (selectedOption[b] !== null){
            checkedInterest = checkedInterest + 1
          }
        }
        if (checkedInterest == 13){
          let InterestCon = document.getElementById("interestsContainer");
          let NextButton = document.getElementById("NextSectionButton");
          let PersonalDiv = document.querySelector('.PersoanlInfoContainer');
          let DayCounter = document.querySelector('#DayCounter');
          PersonalDiv.style.visibility = "hidden"
          DayCounter.style.visibility = "hidden"
          InterestCon.style.visibility = "hidden";
          NextButton.style.visibility = "hidden"
          WYRVisible = true
          

        }
        else{
          alert("Gi din mening på alle interessene")
        }
        
      }
      else{
        alert("Fyll ut aldern din før du går videre")
      }
    }
    else{
      alert("Skriv in navnet ditt før du går videre")
    }
    
  }

  function ShowResault(){
    //Dama ville ha en bedre match score
    if (userName == "Nora" && yearBorn == 2005 && monthValue == 7 && dayValue == 20){
      totalScore = totalScore * 1.4
    }
    //Gjør scoren til et helt tall
    totalScore = Math.floor(totalScore)

    scoreVisible = true
    WYRVisible = false
  }

  function calucluetTotalScore(){
    //Tar scoren fra interessene ganger med 2 og scoren fra WYR og deler på 2 for å finne et greit forhold mellom de 2
    //Deretter ganges summen med 10, som blir trukket fra 100 som gir oss scoren til spillern
    totalScore = (100+((-(endScoreOfInterest*2)) + endScoreOfWYR/2)*10)
    //scoren kan ikke bli over hundre, men potensielt kan den bli under 0, derfor rettes den opp her.
    if (totalScore < 0){
      totalScore = 0
    }
    //hvis alder er under 16 skal man bare ha 80%
    console.log(totalScore, 'befor age')
    if (age < 16){
      totalScore = totalScore * .8
      console.log(totalScore,'under 16')
    }
    if (age > 25){
      totalScore = totalScore * .8
      console.log(totalScore,'over 25')
    }
    if (age > 50){
      totalScore = totalScore * .6
      console.log(totalScore,'over 50')
    }
    else{
      console.log(totalScore)
    }
    ShowResault()
  }

  function checkComperdToMe(user, me){
    //returnerer avstaden mellom svaret mitt til og svaret til brukern 
    return Math.abs(me - user)
  }

  function getScoreWYR(){
    //kjør en loop som går gjennom alle Would you rather spørmål
    for (let a = 0; a < (WhouldYouRatherQ.length/2); a ++ ){
      //hvis svaret mitt ikke er likt som svaret til brukern får brukern 1 minus poeng
      if(WYRMyAnswers[a] !== WhouldYouRatherUserAnswers[a]){
        endScoreOfWYR = endScoreOfWYR - 1
      }
    }
    calucluetTotalScore()
  }

  function getScore(){
    //Definer et nytt array som tar in brukern sine svar som tall istden for tekst
    let userSelctedOptions = []
    let interestScore = 0
    //Skal repetere for hver colone i tabbelen
    for (let i = 0; i < rows.length; i ++){
      //lag et objekt som står for den ene kyen i rows som da er en kolone
      let obj = rows[i]
      //Skal repetere for alle rader i kolonen
      for (let x = 0; x < 5; x ++){
        //sjekker om svaret til brukern passer med noen verider i kolonen
        if (obj.options[x] == selectedOption[i+1]){
          //sett in veriden for matchen, dette gir oss fra 0-4 som matcher med mulige valg
          userSelctedOptions.push(x+1)
          //Slå de sammen, og se på avstadnen mellom bruken sitt svar og mitt.
          interestScore = interestScore +  checkComperdToMe((x+1), mySelectedOption[i])
        }
      }
    }
    //finner gjennomsnittet av brukern sitt svar i forhold til mitt
    endScoreOfInterest = (interestScore/rows.length)
    getScoreWYR()
  }
</script>

<div class="App">
  <div class="PersoanlInfoContainer">
    <input id="InputName" placeholder="Fyll in navnet ditt" type="text" bind:value={userName} on:input={changedName}>

    <p id="AgeText">Velg fødselsdatoen din</p>
    <div class="AgeDefiner">
      <select id="birthYear" bind:value={yearBorn} on:change={yearChange}>
        {#each years as year}
          <option value={year}>{year}</option>
        {/each}
      </select>

      <select name="BirthMonth" id="birthMonth"  bind:value={monthValue} on:change={monthChange}>
        <option value="1">Januar</option>
        <option value="2">Februar</option>
        <option value="3">Mars</option>
        <option value="4">April</option>
        <option value="5">Mai</option>
        <option value="6">Juni</option>
        <option value="7">Juli</option>
        <option value="8">August</option>
        <option value="9">September</option>
        <option value="10">Oktober</option>
        <option value="11">November</option>
        <option value="12">Desember</option>
      </select>
      
      <label id="DayCounter" for="day">{dayValue}.</label>
      <input type="range" id="daySlider" name="day" min="1" max="31" bind:value="{dayValue}" on:change={dayChange}>
      
    </div>
  </div>

  

  <div id="interestsContainer">
    <!--Tabbel for interesser-->
    <table>
      <thead>
        <tr>
          <th>Interesser</th>
          <th id="answerBox">1</th>
          <th id="answerBox">2</th>
          <th id="answerBox">3</th>
          <th id="answerBox">4</th>
          <th id="answerBox">5</th>
          {#if selectedOptionAtAll}
          <th id="svarBox">Svar</th>
          {/if}
        </tr>
      </thead>
      <tbody>
        {#each rows as row}
        <tr>
          <td id="InterestBox">{row.text}</td>
          {#each row.options as option}
          <td>
            <input
              id="intRadioButtons"
              type="radio"
              name="{row.id}"
              value="{option}"
              checked={selectedOption[row.id] === option}
              on:change={handleRadioChange}
            />
          </td>
          {/each}
          {#if selectedOption[row.id] !== null}
          <td>{selectedOption[row.id]}</td>
          {/if}
        </tr>
        {/each}
      </tbody>
    </table>
  </div>
{#if WYRVisible}
  <div id="WouldYouRather">
    {#if WYRQNumber < 2}
      <p id="WYRText">Velg 1 av de kommende dillemaene</p>
    {/if}
    
    <p id="WYRQNumber">{WYRQNumber}/10</p>

    <button id="WYRButton1" on:click={WYRAnswer1}>Vil du ha hvilken som helst super kraft</button>

    <button id="WYRButton2" on:click={WYRAnswer2}>Være den rikeste personen i verden</button>
  </div>
{/if}
  
</div>

<button id="NextSectionButton" on:click={NextSectionFun}>Neste</button>

{#if scoreVisible }
  <div id="ScoreContainer">
    <p id="ScoreText">Her er resultatet: </p>
    <p id="Score">Vi er en {totalScore}% match</p>
  </div>
{/if}


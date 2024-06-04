<html>
	<head>
		<meta name="viewport" content="width=device-width, initial-scale=1.0">
		<style>
        	div.field,div.mas,div.td {
    			display: inline-block;
            }
			table,th,td {
				border: solid;
				text-align: center;
			}
			#runCalculator {
				visibility: hidden;
			}
			#intervalTable {
				visibility: hidden;
			}
		</style>
	</head>
	<h1>Tempo Run Distance Calculator
    </h1>
		<div name="runCalculator" id="runCalculator">
		<h4>Step 1: Enter the distance and time of your most recent time trial. Then press 'Calculate'</h4>
		<label for="dist">Distance:
        </label>
        <br>
  		<input type="number" id="dist" name="dist">
        <select name="d_unit" id="d_unit">
			<option value=" ">
           	</option>
			<option value="mi">mi</option>
			<option value="km">km</option>
		</select>
        <br>
  		<label for="time">Time:
        </label>
        <br>
  		<div name="time" id="time">
        	<div class="field">
            	<input type="number" id="time_min" name="time_min"><br>  	
     		    <label for="time_min">min</label>
        	</div>
            <div class="field">
	            <input type="number" id="time_sec" name="time_sec"><br>
    	        <label for="time_sec">sec</label>
        	</div>
        </div>
        <br>
        <div>
		<button id="calc" name="calc">Calculate</button>
		</div>
		<div id="mas" name="mas" class="mas">
			MAS:
		</div>
		<div id="output" class="mas" type="number"></div>
		</div>
		<br>
	<div id="intervalTable" name="intervalTable">
	 <table>
		 <tr>
			<th colspan="3">Tuesdays</th>
		 </tr>
		 <tr>
		  <th colspan="3">Extensive-Passive Long Intervals</th>
		 </tr>
		 <tr>
			<th colspan="3">Work Interval</th>
		 </tr>
		 <tr>
			 <td>Time(sec)</td>
			 <td>Speed(<div id="tuWorkSpeedUnits" class="td"></div>)</td>
			 <td>Distance(<div id="tuWorkDistUnits" class="td"></div>)</td>
		 </tr>
		 <tr>
			 <td id="tuWorkTime"></td>
			 <td id="tuWorkSpeed"></td>
			 <td id="tuWorkDistance"></td>
		 </tr>
		 <tr>
			 <th colspan="3">Rest Interval</th>
		 </tr>
		 <tr>
			 <td>Time(sec)</td>
			 <td>Speed(<div id="tuRestSpeedUnits" class="td"></div>)</td>
			 <td>Distance(<div id="tuRestDistUnits" class="td"></div>)</td>
		 </tr>
		 <tr>
			 <td id="tuRestTime"></td>
			 <td id="tuRestSpeed"></td>
			 <td id="tuRestDistance"></td>
		 </tr>
	 </table>
	 <br>
	 	 <table>
		 <tr>
			<th colspan="3">Thursdays</th>
		 </tr>
		 <tr>
		  <th colspan="3">Intensive-Passive Short Intervals</th>
		 </tr>
		 <tr>
			<th colspan="3">Work Interval</th>
		 </tr>
		 <tr>
			 <td>Time(sec)</td>
			 <td>Speed(<div id="thWorkSpeedUnits" class="td"></div>)</td>
			 <td>Distance(<div id="thWorkDistUnits" class="td"></div>)</td>
		 </tr>
		 <tr>
			 <td id="thWorkTime"></td>
			 <td id="thWorkSpeed"></td>
			 <td id="thWorkDistance"></td>
		 </tr>
		 <tr>
			 <th colspan="3">Rest Interval</th>
		 </tr>
		 <tr>
			 <td>Time(sec)</td>
			 <td>Speed(<div id="thRestSpeedUnits" class="td"></div>)</td>
			 <td>Distance(<div id="thRestDistUnits" class="td"></div>)</td>
		 </tr>
		 <tr>
			 <td id="thRestTime"></td>
			 <td id="thRestSpeed"></td>
			 <td id="thRestDistance"></td>
		 </tr>
	 </table>
	 </div>
	 <script>
		const show = document.querySelector("#mode");
		const modeValue = show.value;
		const runCalculator = document.querySelector("#runCalculator");
		show.addEventListener('change', (event) => {
			if (event.target.value == "Run"||"Bike"||"Row") {
				runCalculator.style.visibility = 'visible';}
			if (event.target.value == "") {
				runCalculator.style.visibility = 'hidden';
				intervalTable.style.visibility = 'hidden';
				}});

//Work and Rest MAS Percentages
		const tuWorkMAS = .9;
		const tuRestMAS = 0;
		const thWorkMAS = 1.2;
		const thRestMAS = 0;
//Work and Rest Times
		const tuWorkTime = 60;
		const tuRestTime = 30;
		const thWorkTime = 30;
		const thRestTime = 60;	
			


		const speedComp = (tuWorkMAS,miComp) => {
			return   tuWorkMAS* miComp;
			};
		
		const distComp = (tuWorkSpeedComp,tuWorkTime) =>{
			return tuWorkSpeedComp * (tuWorkTime/3600);
			};
		const rowSpeedComp = (time_min,time_sec,tuWorkMAS) => {
			return ((time_min*60+time_sec)/60)*(2-tuWorkMAS);
			};
		const rowDistComp = (time,split) => {
			return ((time/60)/split)*500;
			};
		
        const buttonElement = document.querySelector("button");

        buttonElement.addEventListener("click", (event) => {	
		document.querySelector("#tuWorkTime").innerHTML = tuWorkTime;
		document.querySelector("#tuRestTime").innerHTML = tuRestTime;
		document.querySelector("#thWorkTime").innerHTML = thWorkTime;
		document.querySelector("#thRestTime").innerHTML = thRestTime;
			const miComp = (dist,time_min,time_sec) => {
			return dist/((parseInt(time_min)*60 + parseInt(time_sec))/3600);
		};
        const kmComp = (dist,time_min,time_sec) => {
            return dist/((parseInt(time_min)*60 + parseInt(time_sec))/3600);
        };
		const mComp = (dist,time_min,time_sec) => {
            return (dist/1000)/((parseInt(time_min)*60 + parseInt(time_sec))/3600);
        };
		const rowComp = (dist,time_min,time_sec) => {
			return ((parseInt(time_min)*60 + parseInt(time_sec))/60)/(dist/500);
			};
		const rowCompKM = (dist,time_min,time_sec) => {
			return ((parseInt(time_min)*60 + parseInt(time_sec))/60)/((dist*1000)/500);
			};

			const show = document.querySelector("#mode");
			const modeValue = show.value;
			intervalTable.style.visibility = 'visible'
            const d_unit = document.querySelector("#d_unit");
            const d_unitValue = d_unit.value;
            const inputDist = document.querySelector("#dist");
			const inputTimeMin =  document.querySelector("#time_min");
			const inputTimeSec =  document.querySelector("#time_sec");
            const inputDistValue = inputDist.value;
			const inputTimeMinValue = inputTimeMin.value;
			const inputTimeSecValue = inputTimeSec.value;
			
			if (d_unitValue == "mi" && modeValue == "Run" || "Bike") {
			const outputValue = miComp(inputDistValue,inputTimeMinValue,inputTimeSecValue);
            const output = document.querySelector("#output");

            output.innerHTML = outputValue.toFixed(2)+"mph";

			const speedUnit = document.querySelector("#div.td");
			tuWorkSpeedUnits.innerHTML = "mph";
			tuRestSpeedUnits.innerHTML = "mph";
			tuWorkDistUnits.innerHTML = "mi";
			tuRestDistUnits.innerHTML = "mi";
			thWorkSpeedUnits.innerHTML = "mph";
			thRestSpeedUnits.innerHTML = "mph";
			thWorkDistUnits.innerHTML = "mi";
			thRestDistUnits.innerHTML = "mi";
            const tuWorkSpeedValue = speedComp(tuWorkMAS,outputValue);
			document.querySelector("#tuWorkSpeed").innerHTML=tuWorkSpeedValue.toFixed(2);
			const tuWorkDistanceValue = distComp(tuWorkSpeedValue,tuWorkTime);
			document.querySelector("#tuWorkDistance").innerHTML=tuWorkDistanceValue.toFixed(2);
			const tuRestSpeedValue = speedComp(tuRestMAS,outputValue);
			document.querySelector("#tuRestSpeed").innerHTML=tuRestSpeedValue.toFixed(2);
			const tuRestDistanceValue = distComp(tuRestSpeedValue,tuRestTime);
			document.querySelector("#tuRestDistance").innerHTML=tuRestDistanceValue.toFixed(2);
			const thWorkSpeedValue = speedComp(thWorkMAS,outputValue);
			document.querySelector("#thWorkSpeed").innerHTML=thWorkSpeedValue.toFixed(2);
			const thWorkDistanceValue = distComp(thWorkSpeedValue,thWorkTime);
			document.querySelector("#thWorkDistance").innerHTML=thWorkDistanceValue.toFixed(2);
			const thRestSpeedValue = speedComp(thRestMAS,outputValue);
			document.querySelector("#thRestSpeed").innerHTML=thRestSpeedValue.toFixed(2);
			const thRestDistanceValue = distComp(thRestSpeedValue,thRestTime);
			document.querySelector("#thRestDistance").innerHTML=thRestDistanceValue.toFixed(2);
			};

            if (d_unitValue == "km") {
            const outputValue = kmComp(inputDistValue,inputTimeMinValue,inputTimeSecValue);
            const output = document.querySelector("#output");
            output.innerHTML = outputValue.toFixed(2)+"km/h";
			
			const speedUnit = document.querySelector("#div.td");
			tuWorkSpeedUnits.innerHTML = "km/h";
			tuRestSpeedUnits.innerHTML = "km/h";
			tuWorkDistUnits.innerHTML = "km";
			tuRestDistUnits.innerHTML = "km";
			thWorkSpeedUnits.innerHTML = "km/h";
			thRestSpeedUnits.innerHTML = "km/h";
			thWorkDistUnits.innerHTML = "km";
			thRestDistUnits.innerHTML = "km";
			const tuWorkSpeedValue = speedComp(tuWorkMAS,outputValue);
			document.querySelector("#tuWorkSpeed").innerHTML=tuWorkSpeedValue.toFixed(2);
			const tuWorkDistanceValue = distComp(tuWorkSpeedValue,tuWorkTime);
			document.querySelector("#tuWorkDistance").innerHTML=tuWorkDistanceValue.toFixed(2);
			const tuRestSpeedValue = speedComp(tuRestMAS,outputValue);
			document.querySelector("#tuRestSpeed").innerHTML=tuRestSpeedValue.toFixed(2);
			const tuRestDistanceValue = distComp(tuRestSpeedValue,tuRestTime);
			document.querySelector("#tuRestDistance").innerHTML=tuRestDistanceValue.toFixed(2);
			const thWorkSpeedValue = speedComp(thWorkMAS,outputValue);
			document.querySelector("#thWorkSpeed").innerHTML=thWorkSpeedValue.toFixed(2);
			const thWorkDistanceValue = distComp(thWorkSpeedValue,thWorkTime);
			document.querySelector("#thWorkDistance").innerHTML=thWorkDistanceValue.toFixed(2);
			const thRestSpeedValue = speedComp(thRestMAS,outputValue);
			document.querySelector("#thRestSpeed").innerHTML=thRestSpeedValue.toFixed(2);
			const thRestDistanceValue = distComp(thRestSpeedValue,thRestTime);
			document.querySelector("#thRestDistance").innerHTML=thRestDistanceValue.toFixed(2);
            };
			if (d_unitValue == "meters" ) {
            const outputValue = mComp(inputDistValue,inputTimeMinValue,inputTimeSecValue);
            const output = document.querySelector("#output");
            output.innerHTML = outputValue.toFixed(2)+"km/h";
			
			const speedUnit = document.querySelector("#div.td");
			tuWorkSpeedUnits.innerHTML = "km/h";
			tuRestSpeedUnits.innerHTML = "km/h";
			tuWorkDistUnits.innerHTML = "km";
			tuRestDistUnits.innerHTML = "km";
			thWorkSpeedUnits.innerHTML = "km/h";
			thRestSpeedUnits.innerHTML = "km/h";
			thWorkDistUnits.innerHTML = "km";
			thRestDistUnits.innerHTML = "km";
			const tuWorkSpeedValue = speedComp(tuWorkMAS,outputValue);
			document.querySelector("#tuWorkSpeed").innerHTML=tuWorkSpeedValue.toFixed(2);
			const tuWorkDistanceValue = distComp(tuWorkSpeedValue,tuWorkTime);
			document.querySelector("#tuWorkDistance").innerHTML=tuWorkDistanceValue.toFixed(2);
			const tuRestSpeedValue = speedComp(tuRestMAS,outputValue);
			document.querySelector("#tuRestSpeed").innerHTML=tuRestSpeedValue.toFixed(2);
			const tuRestDistanceValue = distComp(tuRestSpeedValue,tuRestTime);
			document.querySelector("#tuRestDistance").innerHTML=tuRestDistanceValue.toFixed(2);
			const thWorkSpeedValue = speedComp(thWorkMAS,outputValue);
			document.querySelector("#thWorkSpeed").innerHTML=thWorkSpeedValue.toFixed(2);
			const thWorkDistanceValue = distComp(thWorkSpeedValue,thWorkTime);
			document.querySelector("#thWorkDistance").innerHTML=thWorkDistanceValue.toFixed(2);
			const thRestSpeedValue = speedComp(thRestMAS,outputValue);
			document.querySelector("#thRestSpeed").innerHTML=thRestSpeedValue.toFixed(2);
			const thRestDistanceValue = distComp(thRestSpeedValue,thRestTime);
			document.querySelector("#thRestDistance").innerHTML=thRestDistanceValue.toFixed(2);
            };

			if (modeValue == "Row" && d_unitValue == "meters") {
            const outputValue = rowComp(inputDistValue,inputTimeMinValue,inputTimeSecValue);
            const min = Math.floor(outputValue);
 			const sec = (((outputValue) * 60) % 60);
			document.querySelector("#output").innerHTML=min + ":" + (sec < 10 ? "0" : "") + sec +" /500m"; ;
            const tuWorkSpeedValue = rowSpeedComp(min,sec,tuWorkMAS);
			const tuWorkSpeedMin = Math.floor(tuWorkSpeedValue);
 			const tuWorkSpeedSec = Math.floor((tuWorkSpeedValue * 60) % 60);
			document.querySelector("#tuWorkSpeed").innerHTML=tuWorkSpeedMin + ":" + (tuWorkSpeedSec < 10 ? "0" : "") + tuWorkSpeedSec;
			const tuRowWorkDist = rowDistComp(tuWorkTime,tuWorkSpeedValue);
			document.querySelector("#tuWorkDistance").innerHTML= tuRowWorkDist.toFixed(0);

			const thWorkSpeedValue = rowSpeedComp(min,sec,thWorkMAS);
			const thWorkSpeedMin = Math.floor(thWorkSpeedValue);
 			const thWorkSpeedSec = Math.floor((thWorkSpeedValue * 60) % 60);
			document.querySelector("#thWorkSpeed").innerHTML=thWorkSpeedMin + ":" + (thWorkSpeedSec < 10 ? "0" : "") + thWorkSpeedSec;
			const thRowWorkDist = rowDistComp(thWorkTime,thWorkSpeedValue);
			document.querySelector("#thWorkDistance").innerHTML= thRowWorkDist.toFixed(0);

			const speedUnit = document.querySelector("#div.td");
			tuWorkSpeedUnits.innerHTML = "/500m";
			tuRestSpeedUnits.innerHTML = "/500m";
			tuWorkDistUnits.innerHTML = "m";
			tuRestDistUnits.innerHTML = "m";
			thWorkSpeedUnits.innerHTML = "/500m";
			thRestSpeedUnits.innerHTML = "/500m";
			thWorkDistUnits.innerHTML = "m";
			thRestDistUnits.innerHTML = "m";
			if (tuRestMAS == 0) {
				tuRestSpeed.innerHTML="Rest";
				};
			if (tuRestMAS != 0) {
			const tuRestSpeedValue = rowSpeedComp(min,sec,tuRestMAS);
			const tuRestSpeedMin = Math.floor(tuRestSpeedValue);
 			const tuRestSpeedSec = Math.floor((tuRestSpeedValue * 60) % 60);
			document.querySelector("#tuRestSpeed").innerHTML=tuRestSpeedMin + ":"+ (tuRestSpeedSec < 10 ? "0" : "") + tuRestSpeedSec;
			const tuRowRestDist = rowDistComp(tuRestTime,tuRestSpeedValue);
			document.querySelector("#tuRestDistance").innerHTML= tuRowRestDist.toFixed(0);
			};
			if (thRestMAS == 0) {
				thRestSpeed.innerHTML="Rest";
				};
			if (thRestMAS != 0) {
			const thRestSpeedValue = rowSpeedComp(min,sec,thRestMAS);
			const thRestSpeedMin = Math.floor(thRestSpeedValue);
 			const thRestSpeedSec = Math.floor((thRestSpeedValue * 60) % 60);
			document.querySelector("#thRestSpeed").innerHTML=thRestSpeedMin + ":"+ (thRestSpeedSec < 10 ? "0" : "") + thRestSpeedSec;
			const thRowRestDist = rowDistComp(thRestTime,thRestSpeedValue);
			document.querySelector("#thRestDistance").innerHTML= thRowRestDist.toFixed(0);
			};
			};            

			if (modeValue == "Row" && d_unitValue == "km") {
            const outputValue = rowCompKM(inputDistValue,inputTimeMinValue,inputTimeSecValue);
            const min = Math.floor(Math.abs(outputValue));
 			const sec = Math.floor((Math.abs(outputValue) * 60) % 60);
			document.querySelector("#output").innerHTML=min + ":" + (sec < 10 ? "0" : "") + sec +" /500m"; ;
            const tuWorkSpeedValue = rowSpeedComp(min,sec,tuWorkMAS);
			const tuWorkSpeedMin = Math.floor(tuWorkSpeedValue);
 			const tuWorkSpeedSec = Math.floor((tuWorkSpeedValue * 60) % 60);
			document.querySelector("#tuWorkSpeed").innerHTML=tuWorkSpeedMin + ":" + (tuWorkSpeedSec < 10 ? "0" : "") + tuWorkSpeedSec;
			const tuRowWorkDist = rowDistComp(tuWorkTime,tuWorkSpeedValue);
			document.querySelector("#tuWorkDistance").innerHTML= tuRowWorkDist.toFixed(0);

			const thWorkSpeedValue = rowSpeedComp(min,sec,thWorkMAS);
			const thWorkSpeedMin = Math.floor(thWorkSpeedValue);
 			const thWorkSpeedSec = Math.floor((thWorkSpeedValue * 60) % 60);
			document.querySelector("#thWorkSpeed").innerHTML=thWorkSpeedMin + ":" + (thWorkSpeedSec < 10 ? "0" : "") + thWorkSpeedSec;
			const thRowWorkDist = rowDistComp(thWorkTime,thWorkSpeedValue);
			document.querySelector("#thWorkDistance").innerHTML= thRowWorkDist.toFixed(0);

			const speedUnit = document.querySelector("#div.td");
			tuWorkSpeedUnits.innerHTML = "/500m";
			tuRestSpeedUnits.innerHTML = "/500m";
			tuWorkDistUnits.innerHTML = "m";
			tuRestDistUnits.innerHTML = "m";
			thWorkSpeedUnits.innerHTML = "/500m";
			thRestSpeedUnits.innerHTML = "/500m";
			thWorkDistUnits.innerHTML = "m";
			thRestDistUnits.innerHTML = "m";
			if (tuRestMAS == 0) {
				tuRestSpeed.innerHTML="Rest";
				};
			if (tuRestMAS != 0) {
			const tuRestSpeedValue = rowSpeedComp(min,sec,tuRestMAS);
			const tuRestSpeedMin = Math.floor(tuRestSpeedValue);
 			const tuRestSpeedSec = Math.floor((tuRestSpeedValue * 60) % 60);
			document.querySelector("#tuRestSpeed").innerHTML=tuRestSpeedMin + ":"+ (tuRestSpeedSec < 10 ? "0" : "") + tuRestSpeedSec;
			const tuRowRestDist = rowDistComp(tuRestTime,tuRestSpeedValue);
			document.querySelector("#tuRestDistance").innerHTML= tuRowRestDist.toFixed(0);
			};
			if (thRestMAS == 0) {
				thRestSpeed.innerHTML="Rest";
				};
			if (thRestMAS != 0) {
			const thRestSpeedValue = rowSpeedComp(min,sec,thRestMAS);
			const thRestSpeedMin = Math.floor(thRestSpeedValue);
 			const thRestSpeedSec = Math.floor((thRestSpeedValue * 60) % 60);
			document.querySelector("#thRestSpeed").innerHTML=thRestSpeedMin + ":"+ (thRestSpeedSec < 10 ? "0" : "") + thRestSpeedSec;
			const thRowRestDist = rowDistComp(thRestTime,thRestSpeedValue);
			document.querySelector("#thRestDistance").innerHTML= thRowRestDist.toFixed(0);
			};
			};            
        });
    </script>
</html>

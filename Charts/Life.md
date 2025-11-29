
```sqlseal
ADVANCED MODE
CHART

const timezone = 'EST';
let today = new Date();
today.setHours(0,0,0,0);
let year = today.getFullYear();
let birthdayToday = false;

let calendarData = data.map(x => {
	let month = parseInt(x.date.split('-')[0]);
	let day = parseInt(x.date.split('-')[1]);
	let d = new Date(`${year}-${month}-${day}${timezone}`);
	d.setHours(0,0,0,0);
	let c = _color1;
	
	if (today.getTime() == d.getTime()) {
		c = _color4;
		birthdayToday = true;
	}

	return {
		value: [d, 0, x.person],
		itemStyle: { color: c }
	}
});

//add today
if (!birthdayToday) {
	calendarData.push({
		value: [today, 0, 'Today'],
		itemStyle: { color: _color2 }
	});
}

//options definition
let options = {
	grid: _standardGrid,
	legend: { show: false },
	tooltip: _crossTooltip,
	visualMap: { show: false },
	calendar: [
		{
			top: 160,
			left: 50,
			right: 50,
			cellSize: 11.5,
			range: year,
			splitLine: { show: false },
			yearLabel: { show: false },
			monthLabel: { show: false },
			itemStyle: _calendarItemStyle,
			monthLabel: {
				color: '#646464',
				fontFamily: 'Roboto',
				fontSize: 12,
				margin: 10,
				//write out calendar months in numbers instead of words
				nameMap: ['01','02','03','04','05','06','07','08','09','10','11','12'],
			},
			dayLabel: {
				firstDay: 1,
				color: '#646464',
				fontFamily: 'Roboto',
				fontSize: 12,
				margin: 10
			}
		}
	],
	series: [
		{
			type: 'heatmap',
			coordinateSystem: 'calendar',
			data: calendarData,
			itemStyle: { borderRadius: 2 }
		}
	]
};

//style additions + overrides
options.tooltip.formatter = (params) => {
	const d = (params.value[0].getMonth() + 1).toString().padStart(2, '0') + '-' + params.value[0].getDate().toString().padStart(2, '0');

	return `${params.marker}${d}<span style='float: right; margin-left: 20px'><b>${params.value[2]}</b></span>`;
};

return options;

SELECT * FROM birthdays
```
^birthdays

```sqlseal
ADVANCED MODE
CHART

let day = 3600 * 24 * 1000;

//options definition
let options = {
	grid: _standardGrid,
	legend: { show: false },
	tooltip: _crossTooltip,
	dataZoom: _dataZoom,
	xAxis: _cartesianX,
	yAxis: _cartesianY,
	color: _color1,
	series: _lineSeries
};

//style additions + overrides
options.tooltip.formatter = (params) => {
	return `${params.value.Date}</br>${params.marker}${params.value.issue}<span style='float: right; margin-left: 20px'><b>${params.value.severity}</b></span>`;
};

//format axis pointer label to avoid showing data more granular than a single day
options.tooltip.axisPointer.label.formatter = (params) => {
	if (params.axisDimension == 'x') {
		let d = new Date(params.value);
		return d.getFullYear() + '-' + (d.getMonth() + 1).toString().padStart(2, '0') + '-' + d.getDate().toString().padStart(2, '0');
	} else {
		return params.value.toFixed(2);
	}
};

options.xAxis.type = 'time';
options.xAxis.minInterval = day;
options.xAxis.axisLabel.rotate = 0;

options.yAxis.min = 0;
options.yAxis.max = 1;

options.dataZoom.minValueSpan = day * 7;

return options;

//define chart start date here
WITH Dates(date) AS (
	SELECT date('2024-01-01')
	UNION ALL
	SELECT date(date, '+1 day')
	FROM Dates
	WHERE date < CURRENT_DATE
)
SELECT
	d.date AS Date,
	Severity,
	Issue
FROM Dates d LEFT JOIN health h
ON date(h.Date) = date(d.date)
GROUP BY d.date
```
^health

```sqlseal
ADVANCED MODE
CHART

const birth = new Date('2000-01-01');
const death = new Date('2100-01-01'); //assumed date

const start = new Date('2000-01-01');

let lifeData = [];
while (start <= death) {
	let d = new Date(start);
	let live = 0;
	if (d <= new Date() && d >= birth) live = 1;

	lifeData.push([d.getFullYear(), getWeek(d), live]);
	start.setDate(start.getDate() + 7);
}

//will produce duplicate results,
//but duplicate data isn't a problem as it isn't rendered
function getWeek(d) {
	let yearStart = new Date(d.getFullYear(), 0, 1);
	let today = new Date(d.getFullYear(),d.getMonth(),d.getDate());
	let dayOfYear = (today - yearStart + 1) / 86400000;
	let week = Math.ceil(dayOfYear / 6.99); //7 produces odd offsets
	return week;
}

//options definition
let options = {
	grid: _standardGrid,
	legend: { show: false },
	tooltip: _crossTooltip,

	xAxis: {
		type: 'category',
		axisLine: { show: false },
		axisTick: { show: false },
		splitLine: { show: false },
		axisLabel: { show: false }
	},

	yAxis: {
		type: 'category',
		axisLine: { show: false },
		axisTick: { show: false },
		splitLine: { show: false },
		axisLabel: { show: false }
	},
	
	visualMap: {
		show: false,
	    min: 0,
	    max: 1,
	    type: 'piecewise',
	    precision: 0.1,
		splitNumber: 2,
		pieces: [
			{ min: 0, max: 0.1, color: '#242424' },
			{ min: 0.9, max: 1, color: _color1 }
		],
	},
	
	series: [
		{
			type: 'heatmap',
			data: lifeData,
			progressive: 20,
			itemStyle: {
				borderCap: 'round',
				borderJoin: 'round',
				borderColor: '#1E1E1E',
				borderWidth: 2,
				borderRadius: 2
			}
		}
	]
};

//style additions + overrides
options.tooltip.formatter = (params) => {
	return `${params.marker}${params.value[0]}-${params.value[1]}`;
};

return options;

//have to create *some* table
SELECT * FROM files LIMIT 1
```
^life-clock

```sqlseal
TABLE health = file(Health.csv)
GRID
SELECT * from health
```
^health-table

```sqlseal
TABLE birthdays = file(Birthdays.csv)
GRID
SELECT * from birthdays
```
^birthdays-table
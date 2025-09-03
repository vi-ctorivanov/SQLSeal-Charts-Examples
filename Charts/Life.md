
```sqlseal
TABLE health = file(Health.csv)

ADVANCED MODE
CHART

//options definition
let options = {
	grid: _standardGrid,
	legend: { show: false },
	tooltip: _crossTooltip,
	dataZoom: _dataZoom,
	xAxis: _cartesianX,
	yAxis: _cartesianY,
	color: [_color1, _color2, _color3, _color4, _neutralColor],
	series: [
		_lineSeries
	]
}

//style additions + overrides
options.tooltip.formatter = (params) => {
	return `${params.value.Date}</br>${params.marker}${params.value.issue}<span style='float: right; margin-left: 20px'><b>${params.value.severity}</b></span>`;
}

options.xAxis.type = 'time';
options.xAxis.axisLabel.rotate = 0;

options.yAxis.min = 0;
options.yAxis.max = 1;

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
}

//style additions + overrides
options.tooltip.formatter = (params) => {
	return `${params.marker}${params.value[0]}-${params.value[1]}`;
}

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

```sqlseal
CHART {
	grid: _standardGrid,
	legend: _dotLegend,
	tooltip: _crossTooltip,
	dataZoom: _dataZoom,
	xAxis: _cartesianX,
	yAxis: _cartesianY,
	color: [_color1, _color2, _color3, _color4, _neutralColor],
	series: [
		_lineSeries,
		_lineSeries,
		_lineSeries,
		_lineSeries,
		_barSeries
	]
}

SELECT
	substr(strftime('%Y-%m', Date), 3) AS Month,
	SUM(CASE WHEN Division = 'Abstract' THEN Time ELSE 0 END) AS Abstract,
	SUM(CASE WHEN Division = 'Audio' THEN Time ELSE 0 END) AS Audio,
	SUM(CASE WHEN Division = 'Code' THEN Time ELSE 0 END) AS Code,
	SUM(CASE WHEN Division = 'Visual' THEN Time ELSE 0 END) AS Visual,
	SUM(Time) AS 'Total Time'
FROM productivity
GROUP BY Month
ORDER BY Month ASC
```
^productivity

```sqlseal
CHART {
	grid: _standardGrid,
	legend: _dotLegend,
	tooltip: _crossTooltip,
	xAxis: _cartesianX,
	yAxis: _cartesianY,
	color: [_color1, _color2, _color3, _color4],
	series: [
		_barSeries,
		_barSeries,
		_barSeries,
		_barSeries
	]
}

SELECT
	strftime('%m-%d', Date) AS Date,
	SUM(CASE WHEN Division = 'Abstract' THEN Time ELSE 0 END) AS Abstract,
	SUM(CASE WHEN Division = 'Audio' THEN Time ELSE 0 END) AS Audio,
	SUM(CASE WHEN Division = 'Code' THEN Time ELSE 0 END) AS Code,
	SUM(CASE WHEN Division = 'Visual' THEN Time ELSE 0 END) AS Visual
FROM productivity
WHERE Date >= date((SELECT MAX(Date) FROM productivity), '-90 days')
GROUP BY Date
ORDER BY Date ASC
```
^local-productivity

```sqlseal
ADVANCED MODE
CHART

//options definition
let options = {
	grid: _standardGrid,
	legend: _dotLegend,
	tooltip: _crossTooltip,
	dataZoom: _dataZoom,
	xAxis: _cartesianX,
	yAxis: _cartesianY,
	series: [
		{
			//design
			itemStyle: { color: _color1 },
			lineStyle: { color: _color1, width: 1 },
		},
		{
			//linguistics
			itemStyle: { color: _color1 },
			lineStyle: { color: _color1, width: 1, type: 'dashed' }
		},
		{
			//research
			itemStyle: { color: _color1 },
			lineStyle: { color: _color1, width: 1, type: 'dotted' }
		},
		{
			//writing
			itemStyle: { color: _color1 },
			lineStyle: { color: _color1, width: 1, type: 'dashed', dashOffset: 0.3 }
		},
		{
			//composition
			itemStyle: { color: _color2, width: 1 },
			lineStyle: { color: _color2, width: 1 }
		},
		{
			//performance
			itemStyle: { color: _color5, width: 1 },
			lineStyle: { color: _color5, width: 1 }
		},
		{
			//development
			itemStyle: { color: _color3, width: 1 },
			lineStyle: { color: _color3, width: 1 }
		},
		{
			//maintenance
			itemStyle: { color: _color3, width: 1 },
			lineStyle: { color: _color3, width: 1, type: 'dashed' }
		},
		{
			//2D
			itemStyle: { color: _color4, width: 1 },
			lineStyle: { color: _color4, width: 1 }
		},
		{
			//3D
			itemStyle: { color: _color4, width: 1 },
			lineStyle: { color: _color4, width: 1, type: 'dashed' }
		},
		{
			//photography
			itemStyle: { color: _color4, width: 1 },
			lineStyle: { color: _color4, width: 1, type: 'dotted' }
		},
	]
};

//style additions + overrides
for (let i = 0; i < options.series.length; i++) {
	options.series[i].type = 'line';
	options.series[i].symbol = 'circle';
	options.series[i].smooth = 0.2;
}

return options;

SELECT
	substr(strftime('%Y-%m', Date), 3) AS Month,
	
	SUM(CASE WHEN Task = 'Design' THEN Time ELSE null END) AS Design,
	SUM(CASE WHEN Task = 'Linguistics' THEN Time ELSE null END) AS Linguistics,
	SUM(CASE WHEN Task = 'Research' THEN Time ELSE null END) AS Research,
	SUM(CASE WHEN Task = 'Writing' THEN Time ELSE null END) AS Writing,
	
	SUM(CASE WHEN Task = 'Composition' THEN Time ELSE null END) AS Composition,
	
	SUM(CASE WHEN Task = 'Performance' THEN Time ELSE null END) AS Performance,
	
	SUM(CASE WHEN Task = 'Development' THEN Time ELSE null END) AS Development,
	SUM(CASE WHEN Task = 'Maintenance' THEN Time ELSE null END) AS Maintenance,
	
	SUM(CASE WHEN Task = '2D' THEN Time ELSE null END) AS '2D',
	SUM(CASE WHEN Task = '3D' THEN Time ELSE null END) AS '3D',
	SUM(CASE WHEN Task = 'Photography' THEN Time ELSE null END) AS Photography
FROM productivity
GROUP BY Month
ORDER BY Month ASC
```
^task-focus

```sqlseal
CHART {
	grid: _standardGrid,
	legend: _dotLegend,
	tooltip: _crossTooltip,
	dataZoom: _dataZoom,
	xAxis: _cartesianX,
	yAxis: _cartesianY,
	color: [_color1, _color2, _color3, _color4],
	series: [
		_barSeries,
		_barSeries,
		_barSeries,
		_barSeries
	]
}

SELECT
	Project,
	SUM(CASE WHEN Division = 'Abstract' THEN Time ELSE 0 END) AS Abstract,
	SUM(CASE WHEN Division = 'Audio' THEN Time ELSE 0 END) AS Audio,
	SUM(CASE WHEN Division = 'Code' THEN Time ELSE 0 END) AS Code,
	SUM(CASE WHEN Division = 'Visual' THEN Time ELSE 0 END) AS Visual
FROM productivity
GROUP BY Project
ORDER BY Project ASC
```
^project-time

```sqlseal
CHART {
	grid: _standardGrid,
	legend: _dotLegend,
	tooltip: _crossTooltip,
	xAxis: _cartesianX,
	yAxis: _cartesianY,
	color: [_color1, _color2, _color3, _color4],
	series: [
		_barSeries,
		_barSeries,
		_barSeries,
		_barSeries
	]
}

SELECT
	Task,
	SUM(CASE WHEN Division = 'Abstract' THEN Time ELSE 0 END) AS Abstract,
	SUM(CASE WHEN Division = 'Audio' THEN Time ELSE 0 END) AS Audio,
	SUM(CASE WHEN Division = 'Code' THEN Time ELSE 0 END) AS Code,
	SUM(CASE WHEN Division = 'Visual' THEN Time ELSE 0 END) AS Visual
FROM productivity
WHERE Task NOT LIKE '%%%Event%%%' AND Task NOT LIKE '%%%None%%%'
GROUP BY Task
ORDER BY Task ASC
```
^task-time

```sqlseal
CHART {
	legend: _dotLegend,
	tooltip: _crossTooltip,
	color: [_color1, _color2, _color3, _color4],
	series: {
		type: 'pie',
		label: { show: false },
		radius: ['60%', '80%'],
		itemStyle: {
			borderRadius: 3,
			borderColor: '#1E1E1E',
			borderWidth: 4
		},
	}
}

SELECT
	Division AS Divison,
	SUM(Time) AS Time
FROM productivity
WHERE Division NOT LIKE '%%%None%%%'
GROUP BY Division
ORDER BY Division ASC
```
^division-focus

```sqlseal
ADVANCED MODE
CHART

const formattedData = [data.map((x) => x.value)];

//compute maximum because we want to make it the same for all 4 divisions
//and if not set explicitly, echarts automates it to some other value
const maximum = Math.max(...formattedData[0]);

return {
	legend: { show: false },
	tooltip: _crossTooltip,
	radar: {
		indicator: [
			{ name: 'Abstract', max: maximum },
			{ name: 'Audio', max: maximum },
			{ name: 'Code', max: maximum },
			{ name: 'Visual', max: maximum }
		],
		splitNumber: 4,
		axisName: {
			fontFamily: 'Roboto',
			fontSize: 12,
			color: '#646464'
		},
		splitLine: {
			lineStyle: {
				color: [
					_color1,
					_color1 + 20,
					_color1 + 60,
					_color1 + 90,
				]
			}
		},
		splitArea: { show: false },
		axisLine: {
			lineStyle: { color: '#242424', type: 'dashed' }
		}
	},
	series: {
		name: 'Hours',
		type: 'radar',
		data: formattedData,
		label: { show: false },
		itemStyle: { color: _color1 },
		lineStyle: { color: _color1 }
	}
};

SELECT
	SUM(Time) AS value,
	Division AS id
FROM productivity
WHERE Division NOT LIKE '%%%None%%%'
GROUP BY Division
ORDER BY Division ASC
```
^division-time

```sqlseal
ADVANCED MODE
CHART

//options definition
let options = {
	grid: _standardGrid,
	legend: { show: false },
	tooltip: _crossTooltip,
	xAxis: _cartesianY,
	yAxis: _cartesianX,
	color: _color1,
	series: _barSeries
};

//style additions + overrides
options.grid.top = 20;
options.grid.bottom = 40;

return options;

SELECT
	substr(strftime('%Y', Date), 0) AS Year,
	SUM(Time) as Hours
FROM productivity
GROUP BY Year
ORDER BY Year ASC
```
^total-time

```sqlseal
ADVANCED MODE
CHART

return {
	legend: { show: false },
	tooltip: _crossTooltip,
	color: [_color1, _color2, _color4, _color3], //unsure why order is different
	series: [
		{
			type: 'treemap',
			name: 'Project Time',
			//explicitly passing the (already formatted through the query) data 
			//directly to avoid any automated 'dataset' stuff
			data: data,
			colorMappingBy: 'id',
			
			breadcrumb: {
				show: true,
				itemStyle: {
					padding: 5,
					color: '#242424',
					textStyle: {
						fontFamily: 'Roboto',
						fontSize: 12,
						color: '#DADADA'
					}
				},
				emphasis: {
					itemStyle: {
						padding: 5,
						color: '#242424',
						textStyle: {
							fontFamily: 'Roboto',
							fontSize: 13,
							color: '#DADADA'
						}
					},
				}
			},
			roam: false,
			zoomToNodeRatio: 0.2,
			
			left: 25,
			top: 25,
			right: 25,
			bottom: 25,
			
			label: {
				show: true,
				fontFamily: 'Roboto',
				fontSize: 12,
				color: '#FFFFFF'
			},
			itemStyle: { borderColor: '#1E1E1E', gapWidth: 2, borderRadius: 1 }
		}
	]
};

//naming query result names based on what treemaps expects (name, value, id)
WITH DivisionTotals AS (
	SELECT
		Project,
		SUM(Time) AS Hours,
		SUM(CASE WHEN Division = 'Abstract' THEN Time ELSE 0 END) AS Abstract,
		SUM(CASE WHEN Division = 'Audio' THEN Time ELSE 0 END) AS Audio,
		SUM(CASE WHEN Division = 'Code' THEN Time ELSE 0 END) AS Code,
		SUM(CASE WHEN Division = 'Visual' THEN Time ELSE 0 END) AS Visual
	FROM productivity
	GROUP BY Project
)
SELECT
	Project AS name,
	Hours AS value,
CASE 
	WHEN MAX(Abstract, Audio, Code, Visual) = Abstract THEN 'Abstract'
	WHEN MAX(Abstract, Audio, Code, Visual) = Audio THEN 'Audio'
	WHEN MAX(Abstract, Audio, Code, Visual) = Code THEN 'Code'
	WHEN MAX(Abstract, Audio, Code, Visual) = Visual THEN 'Visual'
	END AS id
FROM DivisionTotals
ORDER BY id ASC
```
^project-treemap

```sqlseal
ADVANCED MODE
CHART

function getColor(division) {
	switch (division) {
		case 'Abstract': return _color1;
		case 'Audio': return _color2;
		case 'Code': return _color3;
		case 'Visual': return _color4;
		default: return _color1;
	}
}

//define item style in the data itself so we can have division color-coded days
const divisionData = data.map(x => {
	return {
		value: [x.Date, x.Hours],
		itemStyle: { color: getColor(x.PrimaryDivision) }
	}
});

const hoursData = data.map(x => [x.Date, x.Hours]);
const year = new Date(divisionData[0].value[0] + 'T00:00:00').getFullYear();

//options definition
let options = {
	grid: _standardGrid,
	legend: { show: false },
	tooltip: _crossTooltip,
	visualMap: {
		show: false,
		min: 0,
		max: 12,
		type: 'piecewise',
		orient: 'horizontal',
		precision: 0.1,
		splitNumber: 4,
		pieces: [
			//colors are overridden in top calendar, so this is unique to the bottom one
			{ min: 0.5, max: 2, color: _color4 + 20 },
			{ min: 2, max: 6, color: _color4 + 60 },
			{ min: 6, max: 9, color: _color4 + 90 },
			{ min: 9, max: 12, color: _color4 },
		],
	},
	calendar: [
		{
			top: 100,
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
		},
		{
			top: 200,
			left: 50,
			right: 50,
			cellSize: 11.5,
			range: year,
			splitLine: { show: false },
			yearLabel: { show: false },
			monthLabel: { show: false },
			itemStyle: _calendarItemStyle,
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
			data: divisionData,
			calendarIndex: 0,
			itemStyle: { borderRadius: 2 }
		},
		{
			type: 'heatmap',
			coordinateSystem: 'calendar',
			data: hoursData,
			calendarIndex: 1,
			itemStyle: { borderRadius: 2 }
		}
	]
};

//style additions + overrides
options.tooltip.formatter = (params) => {
	return `${params.marker}${params.value[0].substring(5)}<span style='float: right; margin-left: 20px'><b>${params.value[1]}</b></span>`;
};

return options;

WITH DivisionTotals AS (
	SELECT
		strftime('%Y-%m-%d', Date) AS Date,
		SUM(Time) AS Hours,
		SUM(CASE WHEN Division = 'Abstract' THEN Time ELSE 0 END) AS Abstract,
		SUM(CASE WHEN Division = 'Audio' THEN Time ELSE 0 END) AS Audio,
		SUM(CASE WHEN Division = 'Code' THEN Time ELSE 0 END) AS Code,
		SUM(CASE WHEN Division = 'Visual' THEN Time ELSE 0 END) AS Visual
	FROM productivity
	GROUP BY Date
)
SELECT
	Date,
	Hours,
CASE
	WHEN MAX(Abstract, Audio, Code, Visual) = Abstract THEN 'Abstract'
	WHEN MAX(Abstract, Audio, Code, Visual) = Audio THEN 'Audio'
	WHEN MAX(Abstract, Audio, Code, Visual) = Code THEN 'Code'
	WHEN MAX(Abstract, Audio, Code, Visual) = Visual THEN 'Visual'
	END AS PrimaryDivision
FROM DivisionTotals
WHERE Date >= date((SELECT MAX(Date) FROM productivity), 'start of year')
GROUP BY Date
ORDER BY Date ASC
```
^daily-heatmap

`S> SELECT SUM(Time) FROM productivity` hours
`S> SELECT COUNT(*) FROM productivity` logs
`S> SELECT COUNT(DISTINCT(Date)) FROM productivity` days
^counts

`S> SELECT ROUND(CAST(COUNT(*) AS FLOAT) / COUNT(DISTINCT(Date)), 2) FROM productivity` logs / day
`S> SELECT ROUND(AVG(DailyTotal), 2) FROM (SELECT Date, SUM(Time) AS DailyTotal FROM productivity GROUP BY Date)` hours / day
`S> WITH RecentDays AS (SELECT Date, SUM(Time) AS Days FROM productivity WHERE Date >= date((SELECT MAX(Date) FROM productivity), '-90 days') GROUP BY Date), AllDays AS (SELECT Date, SUM(Time) AS Days FROM productivity GROUP BY Date) SELECT ROUND((SELECT AVG(Days) FROM RecentDays) - (SELECT AVG(Days) FROM AllDays), 2)` hours / day trend
^trend

`S> SELECT SUM(Time) FROM productivity WHERE Date >= date((SELECT MAX(Date) FROM productivity), 'start of year')` hours this year
^year

`S> WITH DivisionTotals AS (SELECT SUM(CASE WHEN Division = 'Abstract' THEN Time ELSE 0 END) AS absTime, SUM(CASE WHEN Division = 'Audio' THEN Time ELSE 0 END) AS audTime, SUM(CASE WHEN Division = 'Code' THEN Time ELSE 0 END) AS codTime, SUM(CASE WHEN Division = 'Visual' THEN Time ELSE 0 END) AS visTime FROM productivity) SELECT ROUND(CAST(absTime AS FLOAT) / (absTime + audTime + codTime + visTime) * 100) FROM DivisionTotals`% abstract, `S> WITH DivisionTotals AS (SELECT SUM(CASE WHEN Division = 'Abstract' THEN Time ELSE 0 END) AS absTime, SUM(CASE WHEN Division = 'Audio' THEN Time ELSE 0 END) AS audTime, SUM(CASE WHEN Division = 'Code' THEN Time ELSE 0 END) AS codTime, SUM(CASE WHEN Division = 'Visual' THEN Time ELSE 0 END) AS visTime FROM productivity) SELECT ROUND(CAST(audTime AS FLOAT) / (absTime + audTime + codTime + visTime) * 100) FROM DivisionTotals`% audio, `S> WITH DivisionTotals AS (SELECT SUM(CASE WHEN Division = 'Abstract' THEN Time ELSE 0 END) AS absTime, SUM(CASE WHEN Division = 'Audio' THEN Time ELSE 0 END) AS audTime, SUM(CASE WHEN Division = 'Code' THEN Time ELSE 0 END) AS codTime, SUM(CASE WHEN Division = 'Visual' THEN Time ELSE 0 END) AS visTime FROM productivity) SELECT ROUND(CAST(codTime AS FLOAT) / (absTime + audTime + codTime + visTime) * 100) FROM DivisionTotals`% code, `S> WITH DivisionTotals AS (SELECT SUM(CASE WHEN Division = 'Abstract' THEN Time ELSE 0 END) AS absTime, SUM(CASE WHEN Division = 'Audio' THEN Time ELSE 0 END) AS audTime, SUM(CASE WHEN Division = 'Code' THEN Time ELSE 0 END) AS codTime, SUM(CASE WHEN Division = 'Visual' THEN Time ELSE 0 END) AS visTime FROM productivity) SELECT ROUND(CAST(visTime AS FLOAT) / (absTime + audTime + codTime + visTime) * 100) FROM DivisionTotals`% visual
^divisions

```sqlseal
TABLE productivity = file(Productivity.csv)
GRID
SELECT * from productivity
```
^productivity-table
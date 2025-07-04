
```sqlseal
TABLE productivity = file(Productivity.csv)

ADVANCED MODE
CHART

const seriesItem = {
	type: 'line',
	symbol: 'circle',
	smooth: 0.2,
	lineStyle: { width: 1 }
}

return {
	grid: {
		show: false,
		left: 50,
		right: 50,
		top: 50,
		bottom: 50
	},
	
	legend: {
		show: true,
		icon: 'circle',
		itemHeight: 5,
		itemWidth: 5,
		inactiveColor: '#363636',
		left: 18,
		top: 10,
		itemGap: 10,
		padding: 5,
		textStyle: {
			fontFamily: 'Roboto',
			fontSize: 0,
			color: '#646464',
			lineHeight: 0
		}
	},
	
	tooltip: {
		show: true,
		padding: 5,
		backgroundColor: '#242424',
		borderColor: 'transparent',
		extraCssText: 'box-shadow: none;',
		textStyle: {
			fontFamily: 'Roboto',
			fontSize: 12,
			color: '#DADADA'
		},
		axisPointer: {
			type: 'cross',
			snap: true,
			label: {
				fontFamily: 'Roboto',
				fontSize: 12,
				color: '#DADADA',
				backgroundColor: '#242424',
				padding: 5
			},
			crossStyle: { color: '#646464' }
		}
	},
	
	xAxis: {
		type: 'category',
		axisLine: { show: false },
		axisTick: { show: false },
		splitLine: { show: false },
		axisLabel: {
			fontFamily: 'Roboto',
			fontSize: 12,
			color: '#646464',
			rotate: 90
		}
	},
	
	yAxis: {
		type: 'value',
		axisLine: { show: false },
		axisTick: { show: false },
		splitLine: { show: false },
		axisLabel: {
			fontFamily: 'Roboto',
			fontSize: 12,
			color: '#646464'
		}
	},
	
	color: ['#FCB97D', '#86BA90', '#778DA9', '#DD7373', '#272D2D'],
	
	series: [
		seriesItem,
		seriesItem,
		seriesItem,
		seriesItem,
		{
			type: 'bar',
			itemStyle: { borderRadius: 1 }
		}
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
ADVANCED MODE
CHART

const seriesItem = {
	type: 'bar',
	stack: 'x',
	itemStyle: { borderRadius: 1 }
}

return {
	grid: {
		show: false,
		left: 50,
		right: 50,
		top: 50,
		bottom: 50
	},
	
	legend: {
		show: true,
		icon: 'circle',
		itemHeight: 5,
		itemWidth: 5,
		inactiveColor: '#363636',
		left: 18,
		top: 10,
		itemGap: 10,
		padding: 5,
		textStyle: {
			fontFamily: 'Roboto',
			fontSize: 0,
			color: '#646464',
			lineHeight: 0
		}
	},
	
	tooltip: {
		show: true,
		padding: 5,
		backgroundColor: '#242424',
		borderColor: 'transparent',
		extraCssText: 'box-shadow: none;',
		textStyle: {
			fontFamily: 'Roboto',
			fontSize: 12,
			color: '#DADADA'
		},
		axisPointer: {
			type: 'cross',
			snap: true,
			label: {
				fontFamily: 'Roboto',
				fontSize: 12,
				color: '#DADADA',
				backgroundColor: '#242424',
				padding: 5
			},
			crossStyle: { color: '#646464' }
		}
	},
	
	xAxis: {
		type: 'category',
		axisLine: { show: false },
		axisTick: { show: false },
		splitLine: { show: false },
		axisLabel: {
			fontFamily: 'Roboto',
			fontSize: 12,
			color: '#646464',
			rotate: 90
		}
	},
	
	yAxis: {
		type: 'value',
		axisLine: { show: false },
		axisTick: { show: false },
		splitLine: { show: false },
		axisLabel: {
			fontFamily: 'Roboto',
			fontSize: 12,
			color: '#646464'
		}
	},

	color: ['#FCB97D', '#86BA90', '#778DA9', '#DD7373'],
	
	series: [
		seriesItem,
		seriesItem,
		seriesItem,
		seriesItem
	]
}

SELECT
	strftime('%m-%d', Date) AS Date,
	SUM(CASE WHEN Division = 'Abstract' THEN Time ELSE 0 END) AS Abstract,
	SUM(CASE WHEN Division = 'Audio' THEN Time ELSE 0 END) AS Audio,
	SUM(CASE WHEN Division = 'Code' THEN Time ELSE 0 END) AS Code,
	SUM(CASE WHEN Division = 'Visual' THEN Time ELSE 0 END) AS Visual
FROM productivity
WHERE Date >= date('now', '-90 days')
GROUP BY Date
ORDER BY Date ASC
```
^local-productivity

```sqlseal
CHART {
	grid: {
		show: false,
		left: 50,
		right: 50,
		top: 50,
		bottom: 50
	},
	
	legend: {
		show: true,
		icon: 'circle',
		itemHeight: 5,
		itemWidth: 5,
		inactiveColor: '#363636',
		left: 18,
		top: 10,
		itemGap: 10,
		padding: 5,
		textStyle: {
			fontFamily: 'Roboto',
			fontSize: 0,
			color: '#646464',
			lineHeight: 0
		}
	},
	
	tooltip: {
		show: true,
		padding: 5,
		backgroundColor: '#242424',
		borderColor: 'transparent',
		extraCssText: 'box-shadow: none;',
		textStyle: {
			fontFamily: 'Roboto',
			fontSize: 12,
			color: '#DADADA'
		},
		axisPointer: {
			type: 'cross',
			snap: true,
			label: {
				fontFamily: 'Roboto',
				fontSize: 12,
				color: '#DADADA',
				backgroundColor: '#242424',
				padding: 5
			},
			crossStyle: { color: '#646464' }
		}
	},
	
	xAxis: {
		type: 'category',
		axisLine: { show: false },
		axisTick: { show: false },
		splitLine: { show: false },
		axisLabel: {
			fontFamily: 'Roboto',
			fontSize: 12,
			color: '#646464',
			rotate: 90
		}
	},
	
	yAxis: {
		type: 'value',
		axisLine: { show: false },
		axisTick: { show: false },
		splitLine: { show: false },
		axisLabel: {
			fontFamily: 'Roboto',
			fontSize: 12,
			color: '#646464'
		}
	},

	color: ['#FCB97D', '#86BA90', '#778DA9', '#DD7373'],
	
	series: [
		{
			//design
			type: 'line',
			symbol: 'circle',
			smooth: 0.2,
			itemStyle: { color: '#FCB97D' },
			lineStyle: { color: '#FCB97D', width: 1 },
		},
		{
			//linguistics
			type: 'line',
			symbol: 'circle',
			smooth: 0.2,
			itemStyle: { color: '#FCB97D' },
			lineStyle: { color: '#FCB97D', width: 1, type: 'dashed' }
		},
		{
			//research
			type: 'line',
			symbol: 'circle',
			smooth: 0.2,
			itemStyle: { color: '#FCB97D' },
			lineStyle: { color: '#FCB97D', width: 1, type: 'dotted' }
		},
		{
			//writing
			type: 'line',
			symbol: 'circle',
			smooth: 0.2,
			itemStyle: { color: '#FCB97D' },
			lineStyle: { color: '#FCB97D', width: 1, type: 'dashed', dashOffset: 0.3 }
		},
		
		{
			//composition
			type: 'line',
			symbol: 'circle',
			smooth: 0.2,
			itemStyle: { color: '#272D2D', width: 1 },
			lineStyle: { color: '#272D2D', width: 1 }
		},
		
		{
			//performance
			type: 'line',
			symbol: 'circle',
			smooth: 0.2,
			itemStyle: { color: '#86BA90', width: 1 },
			lineStyle: { color: '#86BA90', width: 1 }
		},
		
		{
			//development
			type: 'line',
			symbol: 'circle',
			smooth: 0.2,
			itemStyle: { color: '#778DA9', width: 1 },
			lineStyle: { color: '#778DA9', width: 1 }
		},
		{
			//maintenance
			type: 'line',
			symbol: 'circle',
			smooth: 0.2,
			itemStyle: { color: '#778DA9', width: 1 },
			lineStyle: { color: '#778DA9', width: 1, type: 'dashed' }
		},
		
		{
			//2D
			type: 'line',
			symbol: 'circle',
			smooth: 0.2,
			itemStyle: { color: '#DD7373', width: 1 },
			lineStyle: { color: '#DD7373', width: 1 }
		},
		{
			//3D
			type: 'line',
			symbol: 'circle',
			smooth: 0.2,
			itemStyle: { color: '#DD7373', width: 1 },
			lineStyle: { color: '#DD7373', width: 1, type: 'dashed' }
		},
		{
			//photography
			type: 'line',
			symbol: 'circle',
			smooth: 0.2,
			itemStyle: { color: '#DD7373', width: 1 },
			lineStyle: { color: '#DD7373', width: 1, type: 'dotted' }
		},
	]
}

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
ADVANCED MODE
CHART

const seriesItem = {
	type: 'bar',
	stack: 'x',
	itemStyle: { borderRadius: 1 }
}

return {
	grid: {
		show: false,
		left: 50,
		right: 50,
		top: 50,
		bottom: 50
	},
	
	legend: {
		show: true,
		icon: 'circle',
		itemHeight: 5,
		itemWidth: 5,
		inactiveColor: '#363636',
		left: 18,
		top: 10,
		itemGap: 10,
		padding: 5,
		textStyle: {
			fontFamily: 'Roboto',
			fontSize: 0,
			color: '#646464',
			lineHeight: 0
		}
	},
	
	tooltip: {
		show: true,
		padding: 5,
		backgroundColor: '#242424',
		borderColor: 'transparent',
		extraCssText: 'box-shadow: none;',
		textStyle: {
			fontFamily: 'Roboto',
			fontSize: 12,
			color: '#DADADA'
		},
		axisPointer: {
			type: 'cross',
			snap: true,
			label: {
				fontFamily: 'Roboto',
				fontSize: 12,
				color: '#DADADA',
				backgroundColor: '#242424',
				padding: 5
			},
			crossStyle: { color: '#646464' }
		}
	},
	
	xAxis: {
		type: 'category',
		axisLine: { show: false },
		axisTick: { show: false },
		splitLine: { show: false },
		axisLabel: {
			fontFamily: 'Roboto',
			fontSize: 12,
			color: '#646464',
			rotate: 90,
			width: 35,
			overflow: 'truncate',
			ellipsis: '…'
		}
	},
	
	yAxis: {
		type: 'value',
		axisLine: { show: false },
		axisTick: { show: false },
		splitLine: { show: false },
		axisLabel: {
			fontFamily: 'Roboto',
			fontSize: 12,
			color: '#646464'
		}
	},
	
	color: ['#FCB97D', '#86BA90', '#778DA9', '#DD7373'],
	
	series: [
		seriesItem,
		seriesItem,
		seriesItem,
		seriesItem
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
ADVANCED MODE
CHART

const seriesItem = {
	type: 'bar',
	stack: 'x',
	itemStyle: { borderRadius: 1 }
}

return {
	grid: {
		show: false,
		left: 50,
		right: 50,
		top: 50,
		bottom: 50
	},
	
	legend: {
		show: true,
		icon: 'circle',
		itemHeight: 5,
		itemWidth: 5,
		inactiveColor: '#363636',
		left: 18,
		top: 10,
		itemGap: 10,
		padding: 5,
		textStyle: {
			fontFamily: 'Roboto',
			fontSize: 0,
			color: '#646464',
			lineHeight: 0
		}
	},
	
	tooltip: {
		show: true,
		padding: 5,
		backgroundColor: '#242424',
		borderColor: 'transparent',
		extraCssText: 'box-shadow: none;',
		textStyle: {
			fontFamily: 'Roboto',
			fontSize: 12,
			color: '#DADADA'
		},
		axisPointer: {
			type: 'cross',
			snap: true,
			label: {
				fontFamily: 'Roboto',
				fontSize: 12,
				color: '#DADADA',
				backgroundColor: '#242424',
				padding: 5
			},
			crossStyle: { color: '#646464' }
		}
	},
	
	xAxis: {
		type: 'category',
		axisLine: { show: false },
		axisTick: { show: false },
		splitLine: { show: false },
		axisLabel: {
			fontFamily: 'Roboto',
			fontSize: 12,
			color: '#646464',
			rotate: 90,
			width: 35,
			overflow: 'truncate',
			ellipsis: '…'
		}
	},
	
	yAxis: {
		type: 'value',
		axisLine: { show: false },
		axisTick: { show: false },
		splitLine: { show: false },
		axisLabel: {
			fontFamily: 'Roboto',
			fontSize: 12,
			color: '#646464'
		}
	},
	
	color: ['#FCB97D', '#86BA90', '#778DA9', '#DD7373'],
	
	series: [
		seriesItem,
		seriesItem,
		seriesItem,
		seriesItem
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
	legend: {
		show: true,
		icon: 'circle',
		itemHeight: 5,
		itemWidth: 5,
		inactiveColor: '#363636',
		left: 18,
		top: 10,
		itemGap: 10,
		padding: 5,
		textStyle: {
			fontFamily: 'Roboto',
			fontSize: 0,
			color: '#646464',
			lineHeight: 0
		},
		itemStyle: { borderWidth: 0 },
	},
	
	tooltip: {
		show: true,
		padding: 5,
		backgroundColor: '#242424',
		borderColor: 'transparent',
		extraCssText: 'box-shadow: none;',
		textStyle: {
			fontFamily: 'Roboto',
			fontSize: 12,
			color: '#DADADA'
		}
	},

	color: ['#FCB97D', '#86BA90', '#778DA9', '#DD7373'],
	
	series: [
		{
			type: 'pie',
			label: { show: false },
			radius: ['60%', '80%'],
			itemStyle: {
				borderRadius: 3,
				borderColor: '#1E1E1E',
				borderWidth: 4
			},
		}
	]
}

SELECT
	Division,
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
	
	tooltip: {
		show: true,
		padding: 5,
		backgroundColor: '#242424',
		borderColor: 'transparent',
		extraCssText: 'box-shadow: none;',
		textStyle: {
			fontFamily: 'Roboto',
			fontSize: 12,
			color: '#DADADA'
		}
	},
	
	radar: {
		indicator: [
			{ name: 'Abstract', max: maximum },
			{ name: 'Audio', max: maximum },
			{ name: 'Code', max: maximum },
			{ name: 'Visual', max: maximum }
		],
		splitNumber: 4,
		axisName: {
			  color: '#DADADA'
		},
		splitLine: {
			lineStyle: {
				color: [
					'#DADADA',
					'#242424',
					'#363636',
					'#646464'
				]
			}
		},
		splitArea: { show: false },
		axisLine: {
			lineStyle: { color: '#242424', type: 'dashed' }
		}
	},
	
	series: [
		{
			name: 'Hours',
			type: 'radar',
			data: formattedData,
			label: { show: false },
			itemStyle: { color: '#DADADA' },
			lineStyle: { color: '#DADADA' }
		}
	]
}

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
CHART {
	grid: {
		show: false,
		left: 50,
		right: 50,
		top: 20,
		bottom: 50
	},
	
	legend: {
		show: false,
	},
	
	tooltip: {
		show: true,
		padding: 5,
		backgroundColor: '#242424',
		borderColor: 'transparent',
		extraCssText: 'box-shadow: none;',
		textStyle: {
			fontFamily: 'Roboto',
			fontSize: 12,
			color: '#DADADA'
		},
		axisPointer: {
			type: 'cross',
			snap: true,
			label: {
				fontFamily: 'Roboto',
				fontSize: 12,
				color: '#DADADA',
				backgroundColor: '#242424',
				padding: 5
			},
			crossStyle: { color: '#646464' }
		}
	},
	
	xAxis: {
		type: 'value',
		axisLine: { show: false },
		axisTick: { show: false },
		splitLine: { show: false },
		axisLabel: {
			fontFamily: 'Roboto',
			fontSize: 12,
			color: '#646464',
		}
	},
	
	yAxis: {
		type: 'category',
		axisLine: { show: false },
		axisTick: { show: false },
		splitLine: { show: false },
		axisLabel: {
			fontFamily: 'Roboto',
			fontSize: 12,
			color: '#646464'
		}
	},
	
	series: [
		{
			type: 'bar',
			itemStyle: { borderRadius: 1, color: '#DADADA' }
		}
	]
}

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
	
	tooltip: {
		show: true,
		padding: 5,
		backgroundColor: '#242424',
		borderColor: 'transparent',
		extraCssText: 'box-shadow: none;',
		textStyle: {
			fontFamily: 'Roboto',
			fontSize: 12,
			color: '#DADADA'
		}
	},

	color: ['#FCB97D', '#DD7373', '#778DA9', '#86BA90'],
	
	series: [
		{
			type: 'treemap',
			name: 'Project Time',
			//explicitly passing the (already formatted through the query) data 
			//directly to avoid any automated 'dataset' stuff
			data: data, 
			colorMappingBy: "id",
			
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
			
			left: 50,
			top: 50,
			right: 50,
			bottom: 50,
			
			label: {
				show: true,
				fontFamily: 'Roboto',
				fontSize: 12,
				color: '#FFF'
			},
			itemStyle: { borderColor: '#1E1E1E', gapWidth: 2, borderRadius: 1 }
		}
	]
}

//naming query results based on what treemaps expects (name, value, id)
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
	ELSE 'Unknown'
	END AS id
FROM DivisionTotals
ORDER BY id ASC
```
^project-treemap

```sqlseal
ADVANCED MODE
CHART

//define item style in the data itself so we can have division color-coded days
const divisionData = data.map(x => {
	return {
		value: [x.Date, x.Hours],
		itemStyle: { color: x.DivisionColor }
	}
});

const hoursData = data.map(x => [x.Date, x.Hours]);
const year = new Date(divisionData[0].value[0]).getFullYear();

const calendarItemStyle = {
	color: '#242424',
	borderColor: `#1E1E1E`,
	borderWidth: 3,
	borderCap: 'round',
	borderJoin: 'round'
}

return {
	legend: {
		show: false,
	},
	
	tooltip: {
		show: true,
		padding: 5,
		backgroundColor: '#242424',
		borderColor: 'transparent',
		extraCssText: 'box-shadow: none;',
		textStyle: {
			fontFamily: 'Roboto',
			fontSize: 12,
			color: '#DADADA'
		},
		//add color swatch and date to tooltip
		formatter(params) {
			return `${params.marker}${params.value[0].substring(5)}<span style="float: right; margin-left: 20px"><b>${params.value[1]}</b></span>`;
		}
	},
	
	visualMap: {
		show: false,
		min: 0,
		max: 12,
		type: 'piecewise',
		orient: 'horizontal',
		precision: 0.1,
		splitNumber: 4,
		pieces: [
			{ min: 0.5, max: 2, color: '#272D2D' },
			{ min: 2, max: 6, color: '#6E9976' },
			{ min: 6, max: 9, color: '#374C3B' },
			{ min: 9, max: 12, color: '#93CC9E' },
		],
	},
	
	calendar: [
	{
		top: 100,
		left: 50,
		right: 50,
		cellSize: [12, 12],
		range: year,
		splitLine: { show: false },
		yearLabel: { show: false },
		monthLabel: { show: false },
		itemStyle: calendarItemStyle,
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
		cellSize: [12, 12],
		range: year,
		splitLine: { show: false },
		yearLabel: { show: false },
		monthLabel: { show: false },
		itemStyle: calendarItemStyle,
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
}

//directly define colors in the query results to avoid mapping them afterwards
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
	WHEN MAX(Abstract, Audio, Code, Visual) = Abstract THEN '#FCB97D'
	WHEN MAX(Abstract, Audio, Code, Visual) = Audio THEN '#86BA90'
	WHEN MAX(Abstract, Audio, Code, Visual) = Code THEN '#778DA9'
	WHEN MAX(Abstract, Audio, Code, Visual) = Visual THEN '#DD7373'
	ELSE 'Unknown'
	END AS DivisionColor
FROM DivisionTotals
WHERE Date >= date('now', 'start of year')
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
`S> WITH RecentDays AS (SELECT Date, SUM(Time) AS Days FROM productivity WHERE Date >= date('now', '-90 days') GROUP BY Date), AllDays AS (SELECT Date, SUM(Time) AS Days FROM productivity GROUP BY Date) SELECT ROUND((SELECT AVG(Days) FROM RecentDays) - (SELECT AVG(Days) FROM AllDays), 2)` hours / day trend
^trend

`S> SELECT SUM(Time) FROM productivity WHERE Date >= date('now', 'start of year')` hours this year
^year

`S> WITH DivisionTotals AS (SELECT SUM(CASE WHEN Division = 'Abstract' THEN Time ELSE 0 END) AS absTime, SUM(CASE WHEN Division = 'Audio' THEN Time ELSE 0 END) AS audTime, SUM(CASE WHEN Division = 'Code' THEN Time ELSE 0 END) AS codTime, SUM(CASE WHEN Division = 'Visual' THEN Time ELSE 0 END) AS visTime FROM productivity) SELECT ROUND(CAST(absTime AS FLOAT) / (absTime + audTime + codTime + visTime) * 100) FROM DivisionTotals`% abstract, `S> WITH DivisionTotals AS (SELECT SUM(CASE WHEN Division = 'Abstract' THEN Time ELSE 0 END) AS absTime, SUM(CASE WHEN Division = 'Audio' THEN Time ELSE 0 END) AS audTime, SUM(CASE WHEN Division = 'Code' THEN Time ELSE 0 END) AS codTime, SUM(CASE WHEN Division = 'Visual' THEN Time ELSE 0 END) AS visTime FROM productivity) SELECT ROUND(CAST(audTime AS FLOAT) / (absTime + audTime + codTime + visTime) * 100) FROM DivisionTotals`% audio, `S> WITH DivisionTotals AS (SELECT SUM(CASE WHEN Division = 'Abstract' THEN Time ELSE 0 END) AS absTime, SUM(CASE WHEN Division = 'Audio' THEN Time ELSE 0 END) AS audTime, SUM(CASE WHEN Division = 'Code' THEN Time ELSE 0 END) AS codTime, SUM(CASE WHEN Division = 'Visual' THEN Time ELSE 0 END) AS visTime FROM productivity) SELECT ROUND(CAST(codTime AS FLOAT) / (absTime + audTime + codTime + visTime) * 100) FROM DivisionTotals`% code, `S> WITH DivisionTotals AS (SELECT SUM(CASE WHEN Division = 'Abstract' THEN Time ELSE 0 END) AS absTime, SUM(CASE WHEN Division = 'Audio' THEN Time ELSE 0 END) AS audTime, SUM(CASE WHEN Division = 'Code' THEN Time ELSE 0 END) AS codTime, SUM(CASE WHEN Division = 'Visual' THEN Time ELSE 0 END) AS visTime FROM productivity) SELECT ROUND(CAST(visTime AS FLOAT) / (absTime + audTime + codTime + visTime) * 100) FROM DivisionTotals`% visual
^divisions



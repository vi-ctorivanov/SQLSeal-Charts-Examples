
```sqlseal
TABLE resources = file(Finances.csv)

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
		left: 55,
		right: 55,
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
		},
		//ensure the added '$' to the front of the value
		//appears behind a minus '-'
		valueFormatter: function(value) {
			if (value >= 0) return '$' + value.toFixed(2);
			else return '-$' + (value * -1).toFixed(2);
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
		splitLine: { 
			lineStyle: {
				color: '#646464',
				type: 'dashed'
				}
		},
		axisLabel: {
			fontFamily: 'Roboto',
			fontSize: 12,
			color: '#646464',
			//ensure the added '$' to the front of the value 
			//appears behind a minus '-'
			formatter: function(value) {
				if (value >= 0) return '$' + value.toFixed(0);
				else return '-$' + (value * -1).toFixed(0);
			}
			
		}
	},
	
	color: ['#FCB97D', '#86BA90', '#778DA9', '#DD7373', '#272D2D', '#2B2D42'],
	
	series: [
		seriesItem,
		seriesItem,
		seriesItem,
		seriesItem,
		seriesItem,
		seriesItem,
		{
			type: 'line',
			symbol: 'circle',
			smooth: 0.2,
			lineStyle: { color: '#646464', type: 'dashed', width: 1 },
			itemStyle: { color: '#646464' },
		}
	]
}

SELECT
	substr(strftime('%Y-%m', Date), 3) AS Month,
	ROUND(SUM(CASE WHEN Category = 'Housing' THEN Difference ELSE 0 END), 2) AS Housing,
	ROUND(SUM(CASE WHEN Category = 'Services' THEN Difference ELSE 0 END), 2) AS Services,
	ROUND(SUM(CASE WHEN Category = 'Consumables' THEN Difference ELSE 0 END), 2) AS Consumables,
	ROUND(SUM(CASE WHEN Category = 'Desireables' THEN Difference ELSE 0 END), 2) AS Desireables,
	ROUND(SUM(CASE WHEN Category = 'Government' THEN Difference ELSE 0 END), 2) AS Government,
	ROUND(SUM(CASE WHEN Category = 'Work' THEN Difference ELSE 0 END), 2) AS Work,
	ROUND(SUM(Difference), 2) AS Difference
FROM resources
GROUP BY Month
ORDER BY Month ASC
```
^balance

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
		left: 55,
		right: 55,
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
		},
		//ensure the added '$' to the front of the value 
		//appears behind a minus '-'
		valueFormatter: function(value) {
			if (value >= 0) return '$' + value.toFixed(2);
			else return '-$' + (value * -1).toFixed(2);
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
		splitLine: { 
			lineStyle: {
				color: '#646464',
				type: 'dashed'
				}
		},
		axisLabel: {
			fontFamily: 'Roboto',
			fontSize: 12,
			color: '#646464',
			//ensure the added '$' to the front of the value 
			//appears behind a minus '-'
			formatter: function(value) {
				if (value >= 0) return '$' + value.toFixed(0);
				else return '-$' + (value * -1).toFixed(0);
			}
			
		}
	},
	
	color: ['#FCB97D', '#86BA90', '#778DA9', '#DD7373', '#272D2D', '#2B2D42'],
	
	series: [
		seriesItem,
		seriesItem,
		seriesItem,
		seriesItem,
		seriesItem,
		seriesItem,
		{
			type: 'line',
			symbol: 'circle',
			smooth: 0.2,
			lineStyle: { color: '#646464', type: 'dashed', width: 1 },
			itemStyle: { color: '#646464' },
		}
	]
}

SELECT
	substr(strftime('%Y-%m', Date), 3) AS Month,
	ROUND(SUM(CASE WHEN Category = 'Housing' THEN Difference ELSE 0 END), 2) AS Housing,
	ROUND(SUM(CASE WHEN Category = 'Services' THEN Difference ELSE 0 END), 2) AS Services,
	ROUND(SUM(CASE WHEN Category = 'Consumables' THEN Difference ELSE 0 END), 2) AS Consumables,
	ROUND(SUM(CASE WHEN Category = 'Desireables' THEN Difference ELSE 0 END), 2) AS Desireables,
	ROUND(SUM(CASE WHEN Category = 'Government' THEN Difference ELSE 0 END), 2) AS Government,
	ROUND(SUM(CASE WHEN Category = 'Work' THEN Difference ELSE 0 END), 2) AS Work,
	ROUND(SUM(Difference), 2) AS Difference
FROM resources
WHERE Date >= date('now', '-365 days')
GROUP BY Month
ORDER BY Month ASC
```
^local-balance

```sqlseal
TABLE budget = file(Budget.csv)

ADVANCED MODE
CHART

//sunburst requires a parent-children structure,
//for each category, create an array of children,
//where each child is a name+value of an entry in that category in our data
const categories = ['Consumables', 'Desireables', 'Housing', 'Services'];

var formattedData = [];
for (let i = 0; i < categories.length; i++) {
	
	let childData = [];
	for (let j = 0; j < data.length; j++) {
		if (data[j].Category == categories[i]) {
			childData.push(
				{
					name: data[j].Source,
					value: parseFloat(data[j].Yearly)
				}
			);
		}
	}
	
	formattedData.push(
		{
			name: categories[i],
			children: childData
		}
	);
}

return {
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
		valueFormatter: function(value) {
			return '$' + value;
		}
	},
	
	color: ['#86BA90', '#FCB97D', '#DD7373', '#778DA9'],
	
	series: {
	    type: 'sunburst',
	    data: formattedData,
	    radius: ['5%', '90%'],
	    label: {
		    rotate: 'radial',
		    minAngle: 10,
		    fontFamily: 'Roboto',
			fontSize: 12,
			width: 50,
			overflow: 'truncate',
			ellipsis: '…'
	    },
	    itemStyle: {
		    borderColor: '#1E1E1E',
		    borderWidth: 1,
		    borderRadius: 3
	    }
	}
}

SELECT
	Source AS Source,
	Category AS Category,
	Yearly_cost AS Yearly
FROM budget
ORDER BY Category ASC
```
^budget

```sqlseal
ADVANCED MODE
CHART

//define category-to-color system,
//could be made nicer using a library for color modification
function getColor(category, budget=false) {
	switch (category) {
		case 'Consumables':
			if (budget) return '#99A9BE';
			return '#778DA9';
			
		case 'Desireables':
			if (budget) return '#E59696';
			return '#DD7373';
		
		case 'Housing':
			if (budget) return '#FCCA9D';
			return '#FCB97d';
		
		case 'Services':
			if (budget) return '#A4CBAB';
			return '#86BA90';
	}
}

const categoryData = data.map(x => x.Category);

//define colors explicitly in the data
//so that each bar has its intended unique color
const budgetData = data.map(x => {
	return {
		name: 'Budget',
		value: x.MonthlyBudget,
		itemStyle: { color: getColor(x.Category) }
	}
});

const spendingData = data.map(x => {
	return {
		name: 'Spending',
		value: x.MonthlySpending,
		itemStyle: { color: getColor(x.Category, true) }
	}
});

return {
	grid: {
		show: false,
		left: 55,
		right: 55,
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
		},
		valueFormatter: function(value) {
			return '$' + value.toFixed(2);
		}
	},
	
	xAxis: {
		type: 'category',
		data: categoryData,
		axisLine: { show: false },
		axisTick: { show: false },
		splitLine: { show: false },
		axisLabel: {
			fontFamily: 'Roboto',
			fontSize: 12,
			color: '#646464'
		}
	},
	
	yAxis: {
		type: 'value',
		axisLine: { show: false },
		axisTick: { show: false },
		splitLine: {
			lineStyle: {
				color: '#646464',
				type: 'dashed'
				}
		},
		axisLabel: {
			fontFamily: 'Roboto',
			fontSize: 12,
			color: '#646464',
			formatter: function(value, index) {
				return '$' + value.toFixed(0);
			}
		}
	},
	
	series: [
		{
			type: 'bar',
			data: budgetData,
			itemStyle: { borderRadius: 1 }
		},
		{
			type: 'bar',
			data: spendingData,
			itemStyle: { borderRadius: 1 }
		}
	]
}

//create 2 subqueries as we are fetching data from 2 tables,
//and combine them to be processed by our js

//calculate a 3-month average by simply summing the values
//and dividing it by 3
SELECT
	spending.Category,
	spending.MonthlySpending,
	budgeting.MonthlyBudget
FROM (
	SELECT
		Category,
		-ROUND(SUM(Difference) / 3, 2) AS MonthlySpending
	FROM resources
	WHERE Date >= date('now', '-90 days') AND Category NOT LIKE '%%%Work%%%' AND Category NOT LIKE '%%%Government%%%'
	GROUP BY Category
) spending
LEFT JOIN (
	SELECT
		Category,
		SUM(Monthly_cost) AS MonthlyBudget
	FROM budget
	GROUP BY Category
) budgeting ON budgeting.Category = spending.Category
```
^budget-and-spending

$`S> SELECT ROUND(AVG(MonthlyTotal), 2) FROM (SELECT substr(strftime('%Y-%m', Date), 3) AS Month, SUM(Difference) AS MonthlyTotal FROM resources WHERE Date >= date('now', '-90 days') GROUP BY Month)` recent difference / month
^recent-difference
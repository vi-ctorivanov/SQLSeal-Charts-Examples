
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
	color: [_color3, _color1, _color2, _color4, _color5, _color6],
	
	series: [
		_barSeries,
		_barSeries,
		_barSeries,
		_barSeries,
		_barSeries,
		_barSeries,
		{
			type: 'line',
			symbol: 'circle',
			smooth: 0.2,
			lineStyle: { color: _neutralColor, type: 'dashed', width: 1 },
			itemStyle: { color: _neutralColor },
		}
	]
}

//style additions + overrides
options.tooltip.valueForomatter = (value) => {
	if (value >= 0) return '$' + value.toFixed(0);
	else return '-$' + (value * -1).toFixed(0);
};

options.yAxis.splitLine.show = true;
options.yAxis.splitLine.lineStyle = { color: '#646464', type: 'dashed' };
options.yAxis.axisLabel.width = 50;
options.yAxis.axisLabel.formatter = (value) => {
	if (value >= 0) return '$' + value.toFixed(0);
	else return '-$' + (value * -1).toFixed(0);
};

return options;

SELECT
	substr(strftime('%Y-%m', Date), 3) AS Month,
	ROUND(SUM(CASE WHEN Category = 'Housing' THEN Difference ELSE 0 END), 2) AS Housing,
	ROUND(SUM(CASE WHEN Category = 'Services' THEN Difference ELSE 0 END), 2) AS Services,
	ROUND(SUM(CASE WHEN Category = 'Consumables' THEN Difference ELSE 0 END), 2) AS Consumables,
	ROUND(SUM(CASE WHEN Category = 'Desireables' THEN Difference ELSE 0 END), 2) AS Desireables,
	ROUND(SUM(CASE WHEN Category = 'Government' THEN Difference ELSE 0 END), 2) AS Government,
	ROUND(SUM(CASE WHEN Category = 'Work' THEN Difference ELSE 0 END), 2) AS Work,
	ROUND(SUM(Difference), 2) AS Difference
FROM finances
GROUP BY Month
ORDER BY Month ASC
```
^balance

```sqlseal
ADVANCED MODE
CHART

//options definition
let options = {
	grid: _standardGrid,
	legend: _dotLegend,
	tooltip: _crossTooltip,
	xAxis: _cartesianX,
	yAxis: _cartesianY,
	color: [_color3, _color1, _color2, _color4, _color5, _color6],
	series: [
		_barSeries,
		_barSeries,
		_barSeries,
		_barSeries,
		_barSeries,
		_barSeries,
		{
			type: 'line',
			symbol: 'circle',
			smooth: 0.2,
			lineStyle: { color: _neutralColor, type: 'dashed', width: 1 },
			itemStyle: { color: _neutralColor },
		}
	]
}

//style additions + overrides
options.tooltip.valueForomatter = (value) => {
	if (value >= 0) return '$' + value.toFixed(0);
	else return '-$' + (value * -1).toFixed(0);
};

options.xAxis.axisLabel.rotate = 0;

options.yAxis.splitLine.show = true;
options.yAxis.splitLine.lineStyle = { color: '#646464', type: 'dashed' };
options.yAxis.axisLabel.width = 50;
options.yAxis.axisLabel.formatter = (value) => {
	if (value >= 0) return '$' + value.toFixed(0);
	else return '-$' + (value * -1).toFixed(0);
};

return options;

SELECT
	substr(strftime('%Y-%m', Date), 3) AS Month,
	ROUND(SUM(CASE WHEN Category = 'Housing' THEN Difference ELSE 0 END), 2) AS Housing,
	ROUND(SUM(CASE WHEN Category = 'Services' THEN Difference ELSE 0 END), 2) AS Services,
	ROUND(SUM(CASE WHEN Category = 'Consumables' THEN Difference ELSE 0 END), 2) AS Consumables,
	ROUND(SUM(CASE WHEN Category = 'Desireables' THEN Difference ELSE 0 END), 2) AS Desireables,
	ROUND(SUM(CASE WHEN Category = 'Government' THEN Difference ELSE 0 END), 2) AS Government,
	ROUND(SUM(CASE WHEN Category = 'Work' THEN Difference ELSE 0 END), 2) AS Work,
	ROUND(SUM(Difference), 2) AS Difference
FROM finances
WHERE Date >= date('now', '-365 days')
GROUP BY Month
ORDER BY Month ASC
```
^local-balance

```sqlseal
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

//options definition
let options = {
	tooltip: _crossTooltip,
	color: [_color1, _color3, _color2, _color4],
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

//style additions + overrides
options.tooltip.valueFormatter = (value) => {
	return '$' + value;
};

return options;

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

//colors could be made nicer using a library for color modification
//currently, the budget bars are simply 50% opacity
function getColor(category, budget=false) {
	switch (category) {
		case 'Consumables': 
			if (budget) return _color4;
			return _color4 + 80;
			
		case 'Desireables':
			if (budget) return _color2;
			return _color2 + 80;
		
		case 'Housing':
			if (budget) return _color3;
			return _color3 + 80;
		
		case 'Services':
			if (budget) return _color1;
			return _color1 + 80;
		
		default:
			return _color1;
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

//options definition
let options = {
	grid: _standardGrid,
	legend: _dotLegend,
	tooltip: _crossTooltip,
	xAxis: _cartesianX,
	yAxis: _cartesianY,
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

//style additions + overrides
options.tooltip.valueFormatter = (value) => {
	return '$' + value.toFixed(2);
}

options.xAxis.data = categoryData;
options.xAxis.axisLabel.rotate = 0;
options.xAxis.axisLabel.width = 100;

options.yAxis.splitLine.show = true;
options.yAxis.splitLine.lineStyle = { color: '#646464', type: 'dashed' };
options.yAxis.axisLabel.formatter = (value) => {
	return '$' + value.toFixed(0);
};

return options;

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
	FROM finances
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

$`S> SELECT ROUND(AVG(MonthlyTotal), 2) FROM (SELECT substr(strftime('%Y-%m', Date), 3) AS Month, SUM(Difference) AS MonthlyTotal FROM finances WHERE Date >= date('now', '-90 days') GROUP BY Month)` recent difference / month
^recent-difference

```sqlseal
TABLE finances = file(Finances.csv)
GRID
SELECT * from finances
```
^finances-table

```sqlseal
TABLE finances = file(Finances.csv)
GRID
SELECT * from finances
```
^budget-table
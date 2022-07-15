
# Tabular Data Visualization using CHART.Js






```javascript
  <!DOCTYPE html>
<html lang="en">
    <head>
        <title>Fetch and Graph CSV</title>
        <script src="https://cdn.jsdelivr.net/npm/chart.js@3.8.0/dist/chart.min.js"></script>
    </head>
    <body>
        <canvas id="myChart" width="400" height="400"></canvas>
        <script>
            const xlabels = [];
            const ytemps= [];
            updateChart();
            async function updateChart(){
                await getdata();
                const ctx = document.getElementById('myChart').getContext('2d');
            
                const myChart = new Chart(ctx, {
                    type: 'line',
                    data: {
                        labels: xlabels,
                        datasets: [{
                            label: 'GLobal Average Temp in C°',
                            data: ytemps,
                            backgroundColor:'rgba(255, 99, 132, 0.2)',
                            borderColor: 'rgba(255, 99, 132, 1)',
                            borderWidth: 1
                        }]
                    },
                    options: {
                        scales: {
                            y: {
                                ticks: {
                                    
                                    callback: function(value, index, ticks) {
                                        return value+'°';
                                    }
                                }
                            }
                        }
                    }
                    
                });
            }


            async function getdata(){
                const response = await fetch('ZonAnn.Ts+dSST.csv')
                const data = await response.text();
                // console.log(data);

                const table = data.split(/\n/).slice(1);
                // console.log(table)
                table.forEach(row=>{
                    const columns = row.split(',');
                    const year = columns[0];
                    xlabels.push(year)
                    const temp = columns[1];
                    ytemps.push(parseFloat(temp) + 14);
                    console.log(year,temp);
                })
                    
            }
            
        </script>
    </body>
</html>
```


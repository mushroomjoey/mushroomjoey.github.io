<!DOCTYPE html>
<html>
<head>
    <title>PointyBois Transit Center</title>
    <style>
        body { background: #000; color: #fff; font-family: 'Arial', sans-serif; padding: 20px; }
        .board { border: 3px solid #444; background: #111; padding: 15px; width: 400px; border-radius: 10px; margin: 0 auto 20px auto; }
        .header { border-bottom: 2px solid #444; margin-bottom: 15px; padding-bottom: 5px; display: flex; justify-content: space-between; align-items: flex-end; }
        .header h1 { margin: 0; font-size: 1.2rem; text-transform: uppercase; }
        
        /* Titles and Matching Minute Colors */
        .sb-theme { color: #FF99EB; }
        .nb-theme { color: #00f2ff; }

        .arrival-row { display: flex; justify-content: space-between; align-items: center; padding: 12px 0; border-bottom: 1px solid #222; }
        
        /* Unified Fixed-Width Badge */
        .route-num { 
            width: 50px; 
            height: 30px; 
            line-height: 30px; 
            font-weight: bold; 
            border-radius: 4px; 
            text-align: center; 
            font-size: 18px; 
            color: #fff; 
            flex-shrink: 0; 
            box-sizing: border-box;
        }

        .bg-40 { background: #18A300; } 
        .bg-28 { background: #1127EE; } 
        .bg-d  { background: #EE1127; } 
        .bg-default { background: #333; }
        
        .destination { flex-grow: 1; padding-left: 15px; font-size: 16px; color: #eee; white-space: nowrap; overflow: hidden; text-overflow: ellipsis; min-width: 0; }
        .stop-label { font-size: 10px; color: #666; display: block; margin-top: 2px; }
        
        /* Base minute style - color is handled by the render function now */
        .minutes { font-size: 22px; font-weight: bold; width: 100px; text-align: right; flex-shrink: 0; }
        
        /* Gray for Southbound only */
        .too-late-mins { color: #808080 !important; }

        .realtime-icon { color: #39ff14; font-size: 12px; margin-left: 4px; }
        .empty-msg { padding: 20px; text-align: center; color: #666; font-style: italic; font-size: 14px; }
    </style>
</head>
<body>

<div class="board">
    <div class="header">
        <h1 class="sb-theme">PointyBois Transit Center</h1>
        <div id="status-sb" style="font-size: 11px; color: #555;">Connecting...</div>
    </div>
    <div id="arrivals-sb"></div>
</div>

<div class="board">
    <div class="header">
        <h1 class="nb-theme">Arrivals</h1>
        <div id="status-nb" style="font-size: 11px; color: #555;">Connecting...</div>
    </div>
    <div id="arrivals-nb"></div>
</div>

<script>
const STOPS = ["1_40056", "1_28680", "1_28030"];
const API_KEY = "TEST";

async function updateAllStops() {
    try {
        const now = Date.now();
        const twentyMinsFromNow = now + (20 * 60000);
        
        let sbArrivals = [];
        let nbArrivals = [];

        const requests = STOPS.map(stopId => 
            fetch(`https://api.pugetsound.onebusaway.org/api/where/arrivals-and-departures-for-stop/${stopId}.json?key=${API_KEY}`)
            .then(res => res.json())
        );

        const results = await Promise.all(requests);

        results.forEach(data => {
            const stopName = data.data.references.stops.find(s => s.id === data.data.entry.stopId).name;
            const arrivals = data.data.entry.arrivalsAndDepartures;
            
            arrivals.forEach(bus => {
                const timeMs = bus.predictedArrivalTime > 0 ? bus.predictedArrivalTime : bus.scheduledArrivalTime;
                
                if (timeMs >= (now - 60000) && timeMs <= twentyMinsFromNow) {
                    let headsign = bus.tripHeadsign.toUpperCase();
                    
                    if (headsign.includes("DOWNTOWN SEATTLE") && headsign.includes("UPTOWN")) {
                        headsign = "DOWNTOWN SEATTLE";
                    }
                    
                    const isNorthbound = headsign.includes("CROWN HILL") || headsign.includes("CARKEEK");

                    let routeDisplay = bus.routeShortName.toUpperCase();
                    if (routeDisplay.includes("D LINE")) {
                        routeDisplay = "D";
                    }

                    const busObj = {
                        route: routeDisplay,
                        headsign: headsign,
                        time: timeMs,
                        isPredicted: bus.predictedArrivalTime > 0,
                        stop: stopName,
                        vehicleId: bus.vehicleId ? `#${bus.vehicleId.split('_')[1] || bus.vehicleId}` : ""
                    };

                    if (isNorthbound) {
                        nbArrivals.push(busObj);
                    } else {
                        sbArrivals.push(busObj);
                    }
                }
            });
        });

        const renderList = (list, containerId, emptyMsg, showVehicle, isSouthbound, themeColor) => {
            list.sort((a, b) => a.time - b.time);
            const display = document.getElementById(containerId);
            display.innerHTML = "";

            if (list.length === 0) {
                display.innerHTML = `<div class='empty-msg'>${emptyMsg}</div>`;
            } else {
                list.forEach(bus => {
                    const mins = Math.round((bus.time - now) / 60000);
                    
                    // Logic for Southbound Grayout vs Theme Color
                    let colorStyle = `color: ${themeColor};`;
                    if (isSouthbound && mins <= 5) {
                        colorStyle = ""; // CSS class .too-late-mins will take over
                    }
                    
                    const minuteClass = (isSouthbound && mins <= 5) ? "too-late-mins" : "";
                    const timeText = mins <= 0 ? "HERE" : `${mins} MIN`;
                    
                    let colorClass = "bg-default";
                    if (bus.route === '40') colorClass = "bg-40";
                    else if (bus.route === '28') colorClass = "bg-28";
                    else if (bus.route === 'D') colorClass = "bg-d";

                    const subLabel = (showVehicle && bus.vehicleId) ? `Bus ${bus.vehicleId}` : `@ ${bus.stop}`;

                    display.innerHTML += `
                        <div class="arrival-row">
                            <div class="route-num ${colorClass}">${bus.route}</div>
                            <div class="destination">
                                ${bus.headsign}
                                <span class="stop-label">${subLabel}</span>
                            </div>
                            <div class="minutes ${minuteClass}" style="${colorStyle}">
                                ${timeText}${bus.isPredicted ? '<span class="realtime-icon">●</span>' : ''}
                            </div>
                        </div>`;
                });
            }
        };

        // Render Southbound (Pink theme, has grayout)
        renderList(sbArrivals, 'arrivals-sb', 'No Southbound buses.', false, true, '#FF99EB');
        // Render Northbound (Cyan theme, no grayout)
        renderList(nbArrivals, 'arrivals-nb', 'No Northbound buses.', true, false, '#00f2ff');

        const timestamp = "LIVE: " + new Date().toLocaleTimeString();
        document.getElementById('status-sb').innerText = timestamp;
        document.getElementById('status-nb').innerText = timestamp;

    } catch (e) {
        console.error(e);
    }
}

setInterval(updateAllStops, 20000);
updateAllStops();
</script>
</body>
</html>

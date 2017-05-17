# pytrafikverket
python module for communicating with the swedish trafikverket api

## Example
```yaml
from trafikverket_train import TrafikverketTrain, StationInfo
import aiohttp
import asyncio
import async_timeout
from datetime import datetime

async def main(loop):
	async with aiohttp.ClientSession(loop=loop) as session:
		train_api = TrafikverketTrain(loop, "api_key_here")
		stations = await train_api.search_train_stations("kristianstad")
		for station in stations:
			print(station.name + " " + station.signature)

		from_station = await train_api.get_train_station("S�lvesborg")
		to_station = await train_api.get_train_station("Kristianstad C")
		print("from_station_signature: " + from_station.signature)
		print("to_station_signature:   " + to_station.signature)
		train_stop = await train_api.get_train_stop(from_station, to_station, datetime(2017, 5, 15, 12, 57));
		print(train_stop.get_state())

loop = asyncio.get_event_loop()
loop.run_until_complete(main(loop))
```
# Parking-System-Application

User Interface Code
  import React, { useState } from 'react';
import axios from 'axios';
import './CheckAvailabilitySpots.css';
const CheckAvailableSpots = () => {
const [parkingLotName, setParkingLotName] = useState('');
const [vehicleType, setVehicleType] = useState('');
const [availableSpots, setAvailableSpots] = useState(null);
const [errorMessage, setErrorMessage] = useState('');
const handleSubmit = async (e) => {
e.preventDefault();
try {
const response = await
axios.get(http://localhost:8080/availableSpots?parkingLotName=${parkingLotName}&vehicle=${vehicl
eType});
setAvailableSpots(response.data.availableSpots);
} catch (error) {
setErrorMessage('Error fetching available spots');
}
};
return (
<div className='m-5 border border-blue-800 p-2 rounded-lg'>
<h2 className='text-xl font-bold'>Check Available Spots</h2>
<form className='mb-4' onSubmit={handleSubmit}>
<label className='block text-gray-700 text-sm font-bold mb-2'>
Parking Lot Name:
<input className='shadow appearance-none border rounded w-small py-2 px-3 text-gray-700
leading-tight focus:outline-none focus:shadow-outline' type="text" value={parkingLotName}
onChange={(e) => setParkingLotName(e.target.value)} />
</label>
<label className='block text-gray-700 text-sm font-bold mb-2'>
Vehicle Type:
<input className='shadow appearance-none border rounded w-small py-2 px-3 text-gray-700
leading-tight focus:outline-none focus:shadow-outline' type="text" value={vehicleType} onChange={(e)
=> setVehicleType(e.target.value)} />
</label>
<button className='bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded'
type="submit">Check Availability</button>
</form>
{availableSpots !== null && <p className='text-orange-500 text-m italic'>Available Spots:
{availableSpots}</p>}
{errorMessage && <p className='text-red-500 text-m italic'>{errorMessage}</p>}
</div>
);
};
export default CheckAvailableSpots;
import React, { useState } from 'react';
import axios from 'axios';
36
const ParkVehicle = () => {
const [parkingEntityName, setParkingEntityName] = useState('');
const [parkingLotName, setParkingLotName] = useState('');
const [vehicleType, setVehicleType] = useState('');
const [responseMessage, setResponseMessage] = useState('');
const handleSubmit = async (e) => {
e.preventDefault();
try {
const response = await axios.post('http://localhost:8080/parking', {
parkingEntityName,
parkingLotName,
vehicleType,
});
const { ticketId, entryTime, message } = response.data;
setResponseMessage(Ticket ID: ${ticketId}, Entry Time: ${entryTime}, Message: ${message});
} catch (error) {
setResponseMessage('Error parking vehicle');
}
};
return (
<div className='m-5 border border-blue-800 p-2 rounded-lg'>
<h2 className='text-xl font-bold'>Park Vehicle</h2>
<form className='mb-4' onSubmit={handleSubmit}>
<label className='block text-gray-700 text-sm font-bold mb-2'>
Parking Entity Name:
<input className='shadow appearance-none border rounded w-small py-2 px-3 text-gray-700
leading-tight focus:outline-none focus:shadow-outline' type="text" value={parkingEntityName}
onChange={(e) => setParkingEntityName(e.target.value)} />
</label>
<label className='block text-gray-700 text-sm font-bold mb-2'>
Parking Lot Name:
<input className='shadow appearance-none border rounded w-small py-2 px-3 text-gray-700
leading-tight focus:outline-none focus:shadow-outline' type="text" value={parkingLotName}
onChange={(e) => setParkingLotName(e.target.value)} />
</label>
<label className='block text-gray-700 text-sm font-bold mb-2'>
Vehicle Type:
<input className='shadow appearance-none border rounded w-small py-2 px-3 text-gray-700
leading-tight focus:outline-none focus:shadow-outline' type="text" value={vehicleType} onChange={(e)
=> setVehicleType(e.target.value)} />
</label>
<button className='bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded'
type="submit">Park Vehicle</button>
</form>
{responseMessage && <p className='text-orange-500 text-m italic'>{responseMessage}</p>}
</div>
);
};
export default ParkVehicle;
37
import React, { useState } from 'react';
import axios from 'axios';
const UnparkVehicle = () => {
const [ticketId, setTicketId] = useState('');
const [responseMessage, setResponseMessage] = useState('');
const handleSubmit = async (e) => {
e.preventDefault();
try {
const response = await axios.put('http://localhost:8080/unparking', { ticketId });
const {amount, message} = response.data;
setResponseMessage(Amount: ${amount}, Message: ${message});
} catch (error) {
setResponseMessage('Error unparking vehicle');
}
};
return (
<div className='m-5 border border-blue-800 p-2 rounded-lg'>
<h2 className='text-xl font-bold'>Unpark Vehicle</h2>
<form className='mb-4' onSubmit={handleSubmit}>
<label className='block text-gray-700 text-sm font-bold mb-2'>
Ticket ID:
<input className='shadow appearance-none border rounded w-small py-2 px-3 text-gray-700
leading-tight focus:outline-none focus:shadow-outline' type="text" value={ticketId} onChange={(e) =>
setTicketId(e.target.value)} />
</label>
<button className='bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded'
type="submit">Unpark Vehicle</button>
</form>
{responseMessage && <p className='text-orange-500 text-m italic'>{responseMessage}</p>}
</div>
);
};
export default UnparkVehicle;
import React from 'react';
import CheckAvailableSpots from './components/CheckAvailabilitySpots.js';
import ParkVehicle from './components/ParkVehicle.js';
import UnparkVehicle from './components/UnparkVehicle.js';
function App() {
return (
<div>
<h1 className="text-3xl font-bold underline">Parking System</h1>
<CheckAvailableSpots />
<ParkVehicle />
<UnparkVehicle />
</div>
);
}

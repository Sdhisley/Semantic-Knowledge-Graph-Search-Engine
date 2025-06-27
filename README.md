Health Risk Prediction Web App

This project provides a full-stack application for importing patient data into MongoDB, exposing a Health Risk Prediction API, and visualizing results through a React frontend.

Prerequisites
	•	Node.js (v14 or higher)
	•	npm (comes with Node.js)
	•	Docker (for running MongoDB)

Repository Structure

├── backend/                  # Original backend version (v1)
├── backendv2/                # Current backend (v2) with data loader and API server
│   ├── loadData.js           # Script to import patient data into MongoDB
│   ├── server.js             # Express.js API server
│   └── package.json          # Backend dependencies and scripts
├── frontend/                 # React application (Create React App)
│   ├── public/
│   ├── src/
│   ├── package.json
│   └── README.md             # CRA-generated frontend instructions
└── fixed_merged_data.json    # Cleaned patient data for import

Backend Setup (backendv2)
	1.	Pull the MongoDB Docker image

docker pull mongo


	2.	Run MongoDB as a container

docker run --name mongodb-container -d -p 27031:27017 \
  -v mongodbdata:/data/db mongo


	3.	Verify the container is running

docker ps


	4.	Configure environment variables (optional)
Create a .env file in backendv2/ if you wish to override defaults:

PORT=4000
MONGO_URI=mongodb://localhost:27031/patientdb


	5.	Install backend dependencies

cd backendv2
npm install


	6.	Load initial patient data

node loadData.js

This script reads patients.json (from fixed_merged_data.json) and inserts cleaned records into the patients collection in the patientdb database.

	7.	Start the API server

npm start
# or
node server.js

The API will be available at http://localhost:4000 by default.

Frontend Setup
	1.	Navigate to the frontend directory

cd frontend


	2.	Install frontend dependencies

npm install


	3.	Start the React development server

npm start

Open http://localhost:3000 in your browser to view the app.

Usage
	•	Use the API endpoints defined in the backend to fetch or post patient data and risk predictions.
	•	The React app communicates with the backend API to display data and visualization.

Additional Notes
	•	If you need to reset the database, stop and remove the mongodb-container, then repeat the data load step.
	•	Logs for the backend service are written to server.log in backendv2/.

License

This project is licensed under the MIT License.

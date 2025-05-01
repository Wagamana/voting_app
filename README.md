This is a simple voting app designed to demonstrate how microservices can be deployed using Docker Swarm. It consists of several lightweight services working together across a manager and two worker nodes.

The app includes:

A frontend service (vote) where users can vote between two options (A or B). It's accessible via port 5000.
A backend service (result) that displays the current vote counts. It runs on port 5001.
A Redis service that temporarily stores incoming votes from the frontend.
A worker service that transfers votes from Redis into a PostgreSQL database.
The PostgreSQL service (db) stores the actual vote data and uses a persistent volume so that data isn’t lost if the container is restarted or recreated.
The system uses two overlay networks: one for frontend services and one for backend communication, which helps separate concerns and improve security between components.

The db and worker services are restricted to run only on the manager node using Swarm placement constraints. Other services like vote and result are scaled across the cluster for better availability.

To deploy the app, make sure Docker Swarm is initialized on your main node. Then run:

docker stack deploy -c myapp.yml voting_app
Make sure to replace myapp.yml with your actual file name if different.

Once deployed, you can open your browser and go to:

http://<your-server-ip>:5000 to vote
http://<your-server-ip>:5001 to view results
This app is mainly for learning and demonstration purposes, but the same architecture can be used as a foundation for more complex distributed systems.

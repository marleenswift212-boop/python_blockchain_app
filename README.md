# python_blockchain_app
A simple tutorial for developing a blockchain application from scratch in Python.

## What is blockchain? How it is implemented? And how it works?
Please read the step-by-step implementation tutorial to get your answers :)

## Instructions to run
Clone the project,

`$ git clone https://github.com/satwikkansal/python_blockchain_app.git`

Install the dependencies,

`$ cd python_blockchain_app
$ pip install -r requirements.txt`

Start a blockchain node server,

`$ export FLASK_APP=node_server.py
$ flask run --port 8000`

For windows users

`set LANG=C.UTF-8
set FLASK_APP=node_server.py
flask run --port 8000`

One instance of our blockchain node is now up and running at port 8000.

Run the application on a different terminal session,

`$ python run_app.py`

For windows users

`set LANG=C.UTF-8
set FLASK_APP=run_app.py
flask run --port 8000`

The application should be up and running at http://localhost:5000.

Here are a few screenshots

1. Posting some content
<img width="1020" height="427" alt="image" src="https://github.com/user-attachments/assets/cb5d510f-ad61-478c-92a5-f918b5a11042" />


2. Requesting the node to mine

<img width="1022" height="175" alt="image" src="https://github.com/user-attachments/assets/9038b69f-30ae-4857-8c35-b90e6c45dfb9" />


3. Resyncing with the chain for updated data
<img width="1011" height="512" alt="image" src="https://github.com/user-attachments/assets/f657c90a-d402-44db-9f51-f91075f4d4f0" />


To play around by spinning off multiple custom nodes, use the register_with/ endpoint to register a new node.

Here's a sample scenario that you might wanna try,

---
# Make sure you set the FLASK_APP environment variable to node_server.py before running these nodes
# already running
$ flask run --port 8000 &
# spinning up new nodes
$ flask run --port 8001 &
$ flask run --port 8002 &

You can use the following cURL requests to register the nodes at port **8001** and **8002** with the already running **8000**.

`curl -X POST \
  http://127.0.0.1:8001/register_with \
  -H 'Content-Type: application/json' \
  -d '{"node_address": "http://127.0.0.1:8000"}'`
  
`curl -X POST \
  http://127.0.0.1:8002/register_with \
  -H 'Content-Type: application/json' \
  -d '{"node_address": "http://127.0.0.1:8000"}'`
  
This will make the node at port 8000 aware of the nodes at port 8001 and 8002, and make the newer nodes sync the chain with the node 8000, so that they are able to actively participate in the mining process post registration.

To update the node with which the frontend application syncs (default is localhost port 8000), change **CONNECTED_NODE_ADDRESS** field in the views.py file.

Once you do all this, you can run the application, create transactions (post messages via the web inteface), and once you mine the transactions, all the nodes in the network will update the chain. The chain of the nodes can also be inspected by inovking **/chain** endpoint using cURL.

`$ curl -X GET http://localhost:8001/chain
$ curl -X GET http://localhost:8002/chain`

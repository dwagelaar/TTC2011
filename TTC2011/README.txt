This image demonstrates the EMFTVM solution to the TTC 2011 Hello World case
============================================================================

Introduction
------------

This image demonstrates the TTC 2011 Hello World case for EMFTVM. EMFTVM is a model transformation virtual machine for EMF, and is part of the Eclipse ATL project. High-level model transformation languages can be compiled into EMFTVM bytecode. Currently, compilers exist for ATL and SimpleGT (the latter is a simple DPO graph transformation language). The solutions for this case are written in a combination of these two languages

The Eclipse instance contains the solution within the "TTC2011" project:
- TTC2011/metamodels/ contains all relevant metamodels in Ecore format
- TTC2011/models/ contains all (M1) input and output models in XMI format
- TTC2011/transformations/helloworld/ contains all model transformations for the "Hello World" case.

The PDF document viewer shows the original "Hello World" case description. In the remainder of this document, all transformation solutions are discussed one by one.

Task 2.1: Hello World!
----------------------

This task concerns generating a constant - or static - model. For EMFTVM, this task was solved in the ATL language:
- helloworld.atl contains the first part of the task
- helloworld2.atl contains the second part of the task

Endpoint rules are used to generate a constant number of elements.

To run helloworld.atl:
1. Select "Run -> Run Configurations..." from the main menu.
2. Select "ATL EMFTVM Transformation -> helloworld" from the list, and click "Run".

The ATL console shows the execution results. The generated model is called "helloworld.xmi".

To run helloworld2.atl:
1. Select "Run -> Run Configurations..." from the main menu.
2. Select "ATL EMFTVM Transformation -> helloworld2" from the list, and click "Run".

The ATL console shows the execution results. The generated model is called "helloworld2.xmi".

Task 2.2: Count Matches with certain Properties
-----------------------------------------------

As these tasks concern model querying, we use ATL's query mode. No models are generated in this mode, but string values may be printed on the ATL console:
- nrOfNodes.atl counts the amount of nodes
- nrOfLoopingEdges.atl counts the amount of edges with the same src and trg node
- nrOfIsolatedNodes.atl count the amount of nodes without and edge connected to it
- nrOfNodeCircles.atl count the amount of circles of 3 connected nodes
- nrOfDanglingEdges.atl counts the amount of edges with either the src or trg node missing

To run any of these queries:
1. Select "Run -> Run Configurations..." from the main menu.
2. Select "ATL EMFTVM Transformation -> <query name>" from the list, where <query name> corresponds to the query you want to run, and click "Run".

The ATL console shows the requested result. Note that the source model is called "Graph.xmi", in case you want to verify the results manually.

Task 2.3: Reverse Edges
-----------------------

This task concerns updating the source graph, such that all edges point in the other direction (src <-> trg are exchanged). This task has been solved in ATL, as well as in SimpleGT:
- reverseEdgesATL.atl (and graphCopy.atl) copies the input graph, and reverses edges in the process
- reverseEdges.simplegt (and putBackEdgesInGraph.simplegt) uses inplace transformation. Reversed edges are marked with a trace element to prevent the transformation from reversing edges more than once. The generated trace elements are stored in a separate model, which can be discarded afterwards.

To run reverseEdgesATL.atl:
1. Select "Run -> Run Configurations..." from the main menu.
2. Select "ATL EMFTVM Transformation -> reverseEdgesATL" from the list, and click "Run".

The ATL console shows the execution results. The generated model is called "ReversedEdgesGraph.xmi".

To run reverseEdges.simplegt:
1. Make a copy of the model "Graph.xmi", called "Copy of Graph.xmi".
2. Select "Run -> Run Configurations..." from the main menu.
3. Select "ATL EMFTVM Transformation -> reverseEdges" from the list, and click "Run".

The ATL console shows the execution results. The generated model is stored back as "Copy of Graph.xmi".

Task 2.4: Simple Migration
--------------------------

This task migrates a model from one metamodel to another. This is ATL's strong point:
- graphSimpleMigrate.atl migrates a graph from the "graph.ecore" metamodel to the "graph2.ecore" metamodel
- graphTopologyMigrate.atl migrates a graph from the "graph.ecore" metamodel to the "graph3.ecore" metamodel

To run graphSimpleMigrate.atl:
1. Select "Run -> Run Configurations..." from the main menu.
2. Select "ATL EMFTVM Transformation -> graphSimpleMigrate" from the list, and click "Run".

The ATL console shows the execution results. The generated model is called "Graph2.xmi".

Task 2.5: Delete Node with Specific Name and its Incident Edges
---------------------------------------------------------------

This task deletes all nodes named "n1". The provided ATL and SimpleGT solutions also perform the optional task of deleting all incident edges of the "n1" nodes:
- graphDeleteN1.atl copies all graph elements, except for the "n1" nodes and their incident edges
- graphDeleteN1Inplace.simplegt deletes all "n1" incident edges, then deletes all "n1" nodes

To run graphDeleteN1.atl:
1. Select "Run -> Run Configurations..." from the main menu.
2. Select "ATL EMFTVM Transformation -> graphDeleteN1" from the list, and click "Run".

The ATL console shows the execution results. The generated model is called "GraphWithoutN1.xmi".

To run graphDeleteN1Inplace.simplegt:
1. Make a copy of the model "Graph.xmi", called "Copy of Graph.xmi".
2. Select "Run -> Run Configurations..." from the main menu.
3. Select "ATL EMFTVM Transformation -> graphDeleteN1Inplace" from the list, and click "Run".

The ATL console shows the execution results. The generated model is stored back as "Copy of Graph.xmi".

Task 2.6: Optional: Insert Transitive Edges
-------------------------------------------

This task inserts a transitive edge for each pair of connected edges that have an intermediate node in common. A solution is provided in both ATL and SimpleGT:
- graphInsertTransitiveEdges.atl extends the graphCopy.atl transformation, and adds transitive edges where necessary
- graphInsertTransitiveEdgesInplace.simplegt matches the connected edges with common intermediate node, and inserts a transitive edge if it does not yet exist

To run graphInsertTransitiveEdges.atl:
1. Select "Run -> Run Configurations..." from the main menu.
2. Select "ATL EMFTVM Transformation -> graphInsertTransitiveEdges" from the list, and click "Run".

The ATL console shows the execution results. The generated model is called "GraphTransitiveEdges.xmi".

To run graphInsertTransitiveEdgesInplace.simplegt:
1. Make a copy of the model "Graph.xmi", called "Copy of Graph.xmi".
2. Select "Run -> Run Configurations..." from the main menu.
3. Select "ATL EMFTVM Transformation -> graphDeleteN1Inplace" from the list, and click "Run".

The ATL console shows the execution results. The generated model is stored back as "Copy of Graph.xmi".

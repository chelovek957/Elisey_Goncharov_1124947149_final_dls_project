# Elisey_Goncharov_1124947149_final_dls_project


Overview:
This is a research project for DLS school. The topic is Graph Neural Networks and Topological Data Analysis applied to micro-chemistry/physics problems.
In my work the goal was to buld an Equivariant Geometric Neural Network which also utilizes TDA, more precisely Vietoris-Rips complex, to predict HOMO-LUMO energy gaps of molecules. The dataset used was a standard PyG QM9 dataset with around 130000 molecules. And the reserch part is to see how EGNN and TDA help improve predictions, where I built some less complex and compared their performance.


The models used(in order of increasing complexiy):
1) Simple MLP that takes just the atom features as input.
2) A GNN that aggregates information from neighboring atoms via message passing.
3) EGNN that uses relative position vectors scaled by learned scalar functions of distances as geometric input features, ensuring translational and rotational equivariance.
4) An extension of EGNN that additionally incorporates topological features extracted using persistent homology.

About TDA:
For each molecule, persistence diagrams are computed for:
β₀ (connected components)
β₁ (cycles)
(β₂ is included where available but is often empty for small molecules.)
From each persistence diagram, we extract: the count of persistence intervals and the mean lifetime (death − birth) which are then concatenated with learned EGNN representations.

Training:
All models were trained for up to 150 epoch with early stopping based on validation MAE(min_delta=1e-3 and patience=15 epochs).
Best model state selection is based on the best validation performance.

Comparison:

## Results
<table>
  <tr>
  <b>LOSSES</b>
    <td><img src="images/MLPloss.png" width="300">
    <b>MLP</b></td>
    <td><img src="images/gnnloss.png" width="300">
    <b>GNN</b></td>
    <td><img src="images/egnnloss.png" width="300">
    <b>EGNN</b></td>
    <td><img src="images/tdaloss.png" width="300">
    <b>EGNN+TDA</b></td>
  </tr>
  <tr>
  
   <td> <b>METRICS</b><img src="images/mlpmet.png" width="400">
   <b>MLP</b></td>
    <td><img src="images/gnnmet.png" width="400">
    <b>GNN</b></td>
    <td><img src="images/egnnmet.png" width="400">
    <b>EGNN</b></td>
    <td><img src="images/tdamet.png" width="400">
    <b>EGNN+TDA</b></td>
  </tr>
  <tr>
   <td> <b>y_pred vs y_true</b><img src="images/mlpcorr.png" width="400">
   <b>MLP</b></td>
    <td><img src="images/gnncorr.png" width="400">
    <b>GNN</b></td>
    <td><img src="images/egnncorr.png" width="400">
    <b>EGNN</b></td>
    <td><img src="images/tdacorr.png" width="400">
    <b>EGNN+TDA</b></td>
  </tr>
  <tr>
   <td> <b>ERROR DISTRIBUT</b><img src="images/mlperror.png" width="400">
   <b>MLP</b></td>
    <td><img src="images/gnnerror.png" width="400">
    <b>GNN</b></td>
    <td><img src="images/egnnerror.png" width="400">
    <b>EGNN</b></td>
    <td><img src="images/tdaerror.png" width="400">
    <b>EGNN+TDA</b></td>
  </tr>
</table>


## TEST METRICS:

MLP


MAE: 0.8176
RMSE 0.9924

GNN


MAE: 0.2513
RMSE 0.3322

EGNN


MAE: 0.2077
RMSE 0.2768

EGNN+TDA

MAE:  0.1405
RMSE: 0.1862


As we can see from the visuals and the test metrics, indeed the Equivariant Geometric and Topological features boost the model's prediction strength




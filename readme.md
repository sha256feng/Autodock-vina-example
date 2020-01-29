# Autodock Vina for Drug Pose Prediction: a Simple Demo 

The following operations are on a Mac laptop. But they should also work in Linux systems. 

1. Get the vina package 

   ```
    wget http://vina.scripps.edu/download/autodock_vina_1_1_2_linux_x86.tgz
    tar xf autodock_vina_1_1_2_linux_x86.tgz
    cd autodock_vina_1_1_2_linux_x86/bin
    mv vina /Applications/
   ```

2. Prepare the system

   ```
   # Prepare receptor for docking
   ./pythonsh prepare_receptor4.py -r pocket.pdb
   ./pythonsh prepare_ligand4.py -l ligand-b.pdb
   
   # Above codes would generate pdbqt files:
   #     pocket.pdbqt, ligand-b.pdbqt
   ```

3. Configure and run Autodock Vina

   ```
   /Applications/vina --config conf.txt --out out-10modes.pdbqt --log log.txt
   
   # Content of conf.txt: 
   receptor = pocket.pdbqt
   ligand = ligand-b.pdbqt
   
   center_x = 139
   center_y = 145
   center_z = 171
   
   size_x = 25
   size_y = 25
   size_z = 25
   
   num_modes = 10
   ```

   The results PDB file for ligand poses are in "out-10modes.pdbqt", which can be visulized in PyMOL. And the docking summary is like follows:

   ```
   Detected 8 CPUs
   Reading input ... done.
   Setting up the scoring function ... done.
   Analyzing the binding site ... done.
   Using random seed: 838757149
   Performing search ...
   0%   10   20   30   40   50   60   70   80   90   100%
   |----|----|----|----|----|----|----|----|----|----|
   ***************************************************
   done.
   Refining results ... done.
   
   mode |   affinity | dist from best mode
        | (kcal/mol) | rmsd l.b.| rmsd u.b.
   -----+------------+----------+----------
      1         -8.6      0.000      0.000
      2         -7.7      0.926      3.279
      3         -6.7      1.970      7.796
      4         -6.6      2.001      7.587
      5         -6.5      2.610      8.036
      6         -6.4      2.782      8.434
      7         -6.2      6.909      8.542
      8         -6.2      8.815     11.453
      9         -6.1      3.495      6.656
     10         -6.1      6.202     10.949
   Writing output ... done.
   ```

4. MGLtools

   This is for selecting the coordinates and the box for Vina. We can do this directly in PyMOL or VMD. 



## Appendix

Files under this folder:

```
archive/
├── conf.txt                  # Configuration file
├── ligand-b.pdb              # ligand PDB
├── ligand-b.pdbqt            # ligand PDBQT file for vina
├── pocket.pdb                # receptor PDB
├── pocket.pdbqt              # receptor PDBQT file for vina
├── prepare_ligand4.py        # Prepare ligand PDBQT file
├── prepare_receptor4.py      # Prepare protein PDBQT file
├── log.txt                   # Vina log file
├── out-10modes.pdbqt         # Ligand poses file
└── pythonsh                  # Executable python file
```

## Reference 

Vina manual: http://vina.scripps.edu/manual.html

By Shasha Feng, 2020-01.

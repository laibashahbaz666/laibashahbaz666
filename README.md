# Step 1: Prepare input files for the protein-ligand complex
gmx pdb2gmx -f protein_ligand_complex.pdb -o processed.gro -water spce

# Step 2: Energy minimization
gmx grompp -f minim.mdp -c processed.gro -p topol.top -o em.tpr
gmx mdrun -v -deffnm em

# Step 3: Equilibration (NVT ensemble)
gmx grompp -f nvt.mdp -c em.gro -p topol.top -o nvt.tpr
gmx mdrun -v -deffnm nvt

# Step 4: Equilibration (NPT ensemble)
gmx grompp -f npt.mdp -c nvt.gro -p topol.top -o npt.tpr
gmx mdrun -v -deffnm npt

# Step 5: Production MD run
gmx grompp -f md.mdp -c npt.gro -p topol.top -o md.tpr
gmx mdrun -v -deffnm md
# Step 1: Prepare input files for the standalone protein
gmx pdb2gmx -f protein.pdb -o processed_protein.gro -water spce

# Step 2: Energy minimization
gmx grompp -f minim.mdp -c processed_protein.gro -p topol.top -o em_protein.tpr
gmx mdrun -v -deffnm em_protein

# Step 3: Equilibration (NVT ensemble)
gmx grompp -f nvt.mdp -c em_protein.gro -p topol.top -o nvt_protein.tpr
gmx mdrun -v -deffnm nvt_protein

# Step 4: Equilibration (NPT ensemble)
gmx grompp -f npt.mdp -c nvt_protein.gro -p topol.top -o npt_protein.tpr
gmx mdrun -v -deffnm npt_protein

# Step 5: Production MD run
gmx grompp -f md.mdp -c npt_protein.gro -p topol.top -o md_protein.tpr
gmx mdrun -v -deffnm md_protein

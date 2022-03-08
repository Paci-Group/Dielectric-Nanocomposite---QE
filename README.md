# Polarizing_Nanocomp_Project
 Scripts for polarization of nanocomposite materials project. Initial scripts written by David Hally, Updated by Brett Henderson and Archita Adluri.

## Scripts:

1_emin_gram.in --  INITIAL ELECTRON MINIMIZATION WITH GRAM-SCHMIDT ORTHOGONALIZATION.
Stable orthogonalization technique if electrons are far from the minimum but yields incorrect eigenenergies.

2_emin_damp.in -- ZERO-FIELD ELECTRON RELAXATION WITH DAMPED DYNAMICS. Bring electrons to ground-state for initial ion configuration.

3_geom_sd.in -- ZERO-FIELD GEOMETRY OPTIMIZATION WITH STEEPEST DESCENT.  Quickly relax the highest forces.

4_geom_damp.in -- ZERO-FIELD GEOMETRY OPTIMIZATION WITH DAMPED DYNAMICS. Efficiently relax ions once steepest-descent convergence slows down.

5_geom_cell.inn -- # VARIABLE CELL GEOMETRY OPTIMIZATION. Relax lattice vectors to remove stress in the unit cell.

6_geom_nstepe.in -- ZERO-FIELD GEOMETRY OPTIMIZATION WITH CORRECT FORCES. Electrons should now be near minima. this step does final relaxations between ionic movements.

7_zero_field_pol.in -- Calculate microscopic dipole without applied field - used as reference for next steps.

8_efield_electron_pol.in -- macroscopic dipole in presence of a field.

9_efield_ion_pol.in -- Fully allow ion relaxation in presence of a field and calculate dipole.

## How To Run:

Must have peudopotential files, scripts and submission script in the same folder. Fill out all the flags and check with the QuantumEspresso documentation https://www.quantum-espresso.org/Doc/INPUT_CP.html .

## To Check During Calculation:

Steps 4-6 MUST converge fully before continuing to 7-9, increase number of steps otherwise. These scripts assume that the material is an insulator and will most likely fail otherwise. If using QuantumEspresso Versions newer than 6.0, some of the flags/inputs may have changed. Check https://www.quantum-espresso.org/Doc/INPUT_CP.html

Restarting:
Change >ndr flag to current step and restart_mode to 'restart'

## Parts of the scripts:

**ATOMIC_POSITIONS (angstroms)**

Include the .xyz coordinates in angstroms -- no spaces before the coordinates.

**ATOMIC_SPECIES**

Include atomic species label, atomic number and corresponding pseudopotential file name. The pseudopotentials must be copied in the same directory as the .in files. Make sure there are no spaces

Example:
ATOMIC_SPECIES
 O  16.00 O.pz-n-rrkjus_psl.0.1.UPF
 Ag 107.9 Ag.pz-d-rrkjus.UPF
 Mg 24.305 Mg.pz-bhs.UPF

**CELL_PARAMETERS (angstroms)**

Matrix of cell parameters in angstrom. Can obtain from Avogadro or other model-building code.

**Parameters to input/check:**

nbnd= number of bands, see https://www.quantum-espresso.org/Doc/INPUT_CP.html

nat, ntyp  = Number of atoms, number of types of atoms.

ecutwfc and ecutrho - Read pseudopotential file(s) for these.

nr1b, nr2b, nr3b = These are specific to individual crystal structure, pseudopotentials etc... and may not be needed, see https://www.quantum-espresso.org/Doc/INPUT_CP.html

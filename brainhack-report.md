---
event: '2015 OHBM Hackathon (HI)'

title:  'Wrapping FreeSurfer 6 for use in High-performance Computing Environments'

author:

- initials: DGE
  surname: Ellis
  firstname: David G.
  email: hans-johnson@uiowa.edu
  affiliation: aff2
  
- initials: REK
  surname: Kim
  firstname: Regina E.Y.
  email: eunyoung-kim@uiowa.edu
  affiliation: aff3
  
- initials: IO
  surname: Oguz
  firstname: Ipek
  email: ipek-oguz@uiowa.edu
  affiliation: aff4
  
- initials: HJJ
  surname: Johnson
  firstname: Hans J.
  email: hans-johnson@uiowa.edu
  affiliation: aff1,aff3,aff4
  corref: aff1

affiliations:

- id: aff1
  orgname: 'Electrical and Computer Engineering, The University of Iowa'
  street: 4016 Seamans Center for the Engineering Arts and Sciences
  postcode: 52242
  city: Iowa City
  state: Iowa
  country: USA

- id: aff2
  orgname: 'Department of Biomedical Engineering, The University of Iowa'
  street: 1402 Seamans Center for the Engineering Arts and Sciences
  postcode: 52242
  city: Iowa City
  state: Iowa
  country: USA
  
- id: aff3
  orgname: 'Department of Pyschiatry, Carver College of Medicine, The University of Iowa'
  street: 200 Hawkins Drive
  postcode: 52242
  city: Iowa City
  state: Iowa
  country: USA

- id: aff4
  orgname: 'Iowa Institute for Biomedical Imaging, The University of Iowa'
  street: 200 Hawkins Drive
  postcode: 52242
  city: Iowa City
  state: Iowa
  country: USA

url: https://github.com/nipy/nipype

coi: None

acknow: The authors would like to thank the organizers and attendees of the 2015 OHBM Hackathon. This paper is funded by multiple grants Huntington's Disease Society of America (Human Biology Project Fellowship), 3D Shape Analysis for Computational Anatomy (R01 EB008171), Neurobiological Predictors of HD (R01 NS040068), Cognitive and Functional Brain Changes in Preclinical HD (R01 NS054893), Algorithms for Functional and Anatomical Brain Analysis (P41 RR015241), Enterprise Storage in a Collaborative Neuroimaging Environment (S10 RR023392), Core 2b HD (U54 EB005149), and Nipype (R03 EB008673).

contrib: HJJ performed the project and wrote the report. DGE created \texttt{Nipype} interfaces for the FreeSurfer commands, scripted the Nipype workflows, ran the workflow output comparisons, and contributed to the report. IO and RK advised on the project and contributed to the report.
  
bibliography: brainhack-report

gigascience-ref: \href{http://gigadb.org/dataset/100230}{doi:10.5524/100230}
...

#Introduction
FreeSurfer\cite{Fischl2012} is a popular software suite for automatic analysis of MRI data, including subcortical and cortical segmentation, as well as cortical surface reconstruction and correspondence. FreeSurfer's most prominent tool, the \texttt{recon-all} workflow, consists of approximately 170 sequentially run commands in a \texttt{tcsh} shell script that uses approximately 50 unique FreeSurfer tools. The purpose of this project is to reconstruct the  \texttt{recon-all} workflow from FreeSurfer's \texttt{tcsh} shell script into an equivalent workflow using \texttt{Nipype}, which \textit{``supports a uniform interface to existing neuroimaging software and facilitates interaction between these packages within a single workflow''}\cite{Gorgolewski2011}.

The goal of this work is to enhance the efficiency and usability of the workflow by allowing it to take advantage of the increasing availability of high performance computing resources. \texttt{Nipype} also enhances the modularity of the workflow which allows for algorithms from other packages (e.g., ANTS\cite{Avants2009}, FSL\cite{Woolrich2009}, BRAINSTools\cite{YoungKim2013}\cite{Kim2014}\cite{Kim2015}) to be explored, added into the workflow, or take the place of existing processing steps. Therefore, the \texttt{Nipype} environment permits increased collaboration on the \texttt{recon-all} workflow and allows for the limitations of the workflow to be easily addressed.


#Approach
\texttt{Nipype} interfaces were created for the tools used in the \texttt{recon-all} workflow. These interfaces allow developers to recreate in a  \texttt{Nipype} workflow the exact same commands used in the FreeSurfer's \texttt{tcsh} script. The \texttt{Nipype} version of the \texttt{recon-all} workflow was then created by using the \texttt{Nipype} interfaces to connect the FreeSurfer commands in the order necessary. To verify that the new \texttt{Nipype} workflow is equivalent to FreeSurfer's \texttt{recon-all} workflow, both workflows were run on the same set of MRI images on multiple platforms (CentOS 6.4 and Mac OS X) and in a high-performance computing environment. Output surface files were converted to VTK file format, and the output image files were converted to NIFTI file format. The images and surfaces output from FreeSurfer's \texttt{recon-all} workflow were compared to the outputs from  \texttt{Nipype} \texttt{recon-all} workflow.

#Results
All output images and surfaces from FreeSurfer's \texttt{recon-all} were identical to those of the \texttt{Nipype} workflow that was run on the same operating system. During testing on a 16 Core CentOS 6.4 machine with 64GB of memory, FreeSurfer's \texttt{recon-all} workflow completed processing in over 8.9 hours. With multiprocessing, the \texttt{Nipype} workflow achieved identical results and completed processing in under 6 hours when tested on the same machine.

\begin{figure}[h]
\centering
\includegraphics[width=.45\textwidth]{FS6NipypeDiff.png}
\caption{Visualization of the cortical thickness projected onto the left hemisphere's inflated surface for both the FreeSurfer(left) and \texttt{Nipype}(middle) workflows as well as the difference the two thicknesses(right). The thickness measurements showed no difference between the workflows.}
\end{figure}

# Conclusions
The \texttt{Nipype} workflow created in this project was shown to be equivalent to the pre-existing FreeSurfer \texttt{recon-all} workflow. Furthermore, by utilizing \texttt{Nipype}'s ability to run commands in parallel, the new workflow reduces the running time of \texttt{recon-all} by over 30\% when compared to FreeSurfer's \texttt{recon-all} script which runs commands in a sequential order. The \texttt{Nipype} environment also allows for increased collaboration in further developing the workflow. Future work will involve incorporating more options to the \texttt{Nipype} workflow so that it can function as a complete replacement for the \texttt{tcsh} shell script. The collaborations at the 2015 OHBM BrainHack meeting were instrumental in accomplishing this task. Collaborations with the FreeSurfer, \texttt{Nipype}, and Human Connectome teams allowed members of this project to quickly identify problems and avoid unnecessary failures.
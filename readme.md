# Dataset
This dataset corresponds to our **TSE work (Under review)**. We provided the benchmarks collected from 499 open source projects for continued research of possible dependencies due to dynamic typing in Python software.

We extended our previous tool **ENRE** to extract *possible dependencies* from source code. The version supporting posisble dependency extraction is [**ENRE2.0**](https://github.com/xjtu-enre/ENRE-go-python/tree/v2.0)

**Due to the large size of our data,  we have put the whole dataset of 499 projects on OneDrive, you can download it [HERE](https://1drv.ms/u/s!AoXM5AoG1Law1TWnRm8vlMxuGlaL?e=IfaJNl)**

In the current repository in GutHUb, except for *project_analysis* folder, the other folders contains the whole data used in our work.  *project_analysis* folder contains the tool analysis results of the first 20 projects (in alphabetical order) out of 499 projects. You can download the whole set from the above [**LINK**](https://1drv.ms/u/s!AoXM5AoG1Law1TWnRm8vlMxuGlaL?e=IfaJNl) 

Now we introduce the dataset as follows.

## 1. project_list 

**project_list** folder includes all the project information we have studied. Now we introduce the five files under this folder:

We initially collected 864 projects with their latest versions. All the 864 projects are listed in **ProjectList1-864.csv**.

Since our study required a well-managed revision history, we filtered out projects with fewer than 100 commits.  After this step, there were  704 projects remaining. **ProjectList2-704.csv**  lists these projects. 

Next, we removed the repeated or forked projects, and tutorial projects if their textual description contains the keywords *tutor|tutorial|course|exercise|guide|note|demo|example|sample*. After this operation, there were 665 projects remaining.  **ProjectList3-665.csv**  lists these projects. 

We further excluded small projects where the number of files is smaller than 40 or the number of Python files is smaller than 8. In the end we collected 499 projects as the subjects of our study, which are listed in **ProjectList4-499.csv**.

All these "\*.csv" files list the information of each project, including project ***name***, ***Url***,  ***Description***, the number of ***files***,  ***Loc*** (Lines of Code), the number of ***commits***, the numer of ***issueCommits*** (issue-related commits), the number of ***committers***, the number of ***issueCommiters*** (issue-related committers),  the number of ***PyFiles*** (python files), ***PyLoc*** (Python Loc), and the average python Loc per file (***AvgLoCPerFile***). The summary of these information corresponds to *Table 2* and *Figure 6* in our paper draft.

To analyze the domain of these 499 projects, we recruited five research volunteers (including one PhD student and four other graduate students) to label the domain of each Python project, following the  application domain categories introduced in Python official community ({https://legacy.python.org/about/apps/}). To mitigate any subjectivity threat, they cross-validated their results and reached consensus after an independent labeling step.  The domain information is listed in **ProjectList4-499-domain.xlsx**.  The summary of domain distribution corresponds to *Table 3* in our paper draft.


## 2. project_analysis

Each folder under this directory corresponds to  the raw data of  an individual project. The data are obtained from analyzing the source code and revision history by employing diverse tools (i.e., **[SCITool Understand](https://scitools.com/)**, **[ENRE](https://github.com/xjtu-enre/ENRE-go-python/)**, **[DV8](https://archdia.com)**) used in our study. Since the entire size of all 499 projects' analysis results is large, we upload the data of the first 20 projects in this github repository. You can obtain all of the 499 projects from our onedrive share [link](https://1drv.ms/u/s!AoXM5AoG1Law1TWnRm8vlMxuGlaL?e=IfaJNl))

Under each sub-folder,
### 2.1 *dsm* and *new_dsm*folders
 
*dsm* contains the file-level dependencies in DSM using Json file. In this folder:

--*$projectname$_his.json* is the dependency results (**co-change relations**) from revision history.

--*$projectname$_und_XX* is the dependencies results (i.e., **explicit dependencies**) by using Understand.

--*$projectname$_und_P1_XX$* is the dependencies results (i.e., **P1 possible  dependencies**) by using ENRE 2.0.

*new_dsm* folder contains the dependency results by merging two dependency files from $dsm$ folder.

### 2.2 maintenance measurements based on DL and PC metrics

*$projectname$_PC.json* is the PC (Propagation Cost)measurement of this $projectname$ based on explicit file-level dependencies only.

*$projectname$_P1_PC.json* is the PC measurement of this $projectname$ based on explicit file-level dependencies and possible (P1) file-level dependencies.

*$projectname$_DL.json* is the DL (Decoupling Level) measurement of this $projectname$ based on explicit file-level dependencies only.

*$projectname$_P1_DL.json* is the DL measurement of this $projectname$ based on explicit file-level dependencies and possible (P1) file-level dependencies.

### 2.3 *mc* folder: maintenance costs computed based on mining revision history.

*file-loc.csv* is the size information

*file-mc.csv* is the maintenance cost of each source file of a project.

*gitlog* is the git log exported from git of a project.

*history-py.csv* contains the changed file set and issue-fixed related information for each revision commit of a prpject.

*changecost* is the change cost of a project.

### 2.4  *archissue* folder: architecture anti-pattern detection results 

*archissue-und-6* contains the anti-patter instances detected based on explicit dependencies only.

*archissue-und-p1-6* contains the anti-patter instances detected based on explicit dependencies and possible dependencies (the union of them).

each subfolder inside *archissue-und-6* or *archissue-und-p1-6* corresponds to the instances of each anti-pattern.  

Our work studied the six kinds of anti-patterns, i.e., clique (CLQ), modularity-violation (MVG), packgae-cycle (PKG), unhealthy-inheritance (UHI), unstable-interface (UIF), and crossing (CRS). If a corresponding folder of an anti-pattern is missing, it means that this project does not present this anti-pattern when using the experimental settings.




## 3. analysis_results

This folder lists the analysis results based on the raw data for each RQ.

### 3.1 RQ1

1) Benchmark A

**benchmarkA.csv** lists the bechmarks obtained from the projects, by following the benchmark collection methods introduced in *Section 3.4.1 The setup for RQ1--1) Benchmark Generation--Cochange Benchmark A*. 

**benchmarkA-results.csv** lists the precision and recall results against the benchmarkA. F1 scores can be calculated based on precision and recall.

For all 20 benchmarks (h1-h20) in the benchmarkA, we used 301 of the 499 projects as subjects because we can obtain all the required benchmark data from their revision histories. The other 198 projects were excluded as several benchmarks were unavailable given the rigorous parameter settings.

2) Benchmark B

**benchmarkB.csv** lists the bechmarks obtained from the projects, by following the benchmark collection methods introduced in *Section 3.4.1 The setup for RQ1--1) Benchmark Generation--Cochange Benchmark B*. 

**benchmarkA-results.csv** lists the precision and recall results against the benchmarkA. F1 scores can be calculated based on precision and recall.

For all  benchmarks in the benchmarkB, we used 301 of the 499 projects as subjects because we can obtain all the required benchmark data from their revision histories, given the rigorous parameter settings.

### 3.2 RQ2

**summary_dl.xlsx** lists the DL (the Dependency Level) scores of all projects.

**summary_pc.xlsx** lists the PC (the Propagation Cost) scores of all projects.

DL and PC metrics are two state-of-the-art architectural maintainability metrics, which are calculated based on file-level dependencies.

**mc-groundtruth.csv**  lists the maintenance cost computed based on revision history, including six metrixs and they are BPCO, BPCO, CCOR, BCOR, CCFOR, and BCFOR. These measurements are considered as the groundtruth.

**summary_filetype_mc_issuenum.csv** lists the *K_issue* measurements  which are the rates of file_p1 to file_e.

**summary_filetype_mc_issueloc.csv** lists the *K_issueLoc* measurements  which are the rates of file_p1 to file_e.

**summary_filetype_mc_issuecmt.csv** lists the *K_issueCmt* measurements  which are the rates of file_p1 to file_e.

**summary_filetype_mc_cmt.csv** lists the *K_cmt* measurements  which are the rates of file_p1 to file_e.

**summary_filetype_mc_changeloc.csv** lists the *K_loc* measurements  which are the rates of file_p1 to file_e.

**summary_filetype_mc_authornum.csv** lists the *K_author* measurements  which are the rates of file_p1 to file_e.


### 3.3 RQ3

**archissue-instance-affectedfiles.csv** lists the number of instances and affected files involved in atchitecture anti-patterns, including  UIF, UHI, MVG, CRS, PKG, and CLQ. We analyzed these data to observe the anti-patterns when considering possible dependencies.

**archissue-mc.csv** lists the maitence cost of files invovled in anti-patterns vs. non-affected files, which are used to calculate the *increase* and *\delta increase* for anti-pattern verification.

**archissue-CLQ-infect-bydep.csv** lists the maintenance cost (in terms of six metrics) of file_e, file_p1, and file_e_p1 for CLQ anti-pattern.

**archissue-CRS-infect-bydep.csv** lists the maintenance cost (in terms of six metrics) of file_e, file_p1, and file_e_p1 for CRS anti-pattern.

**archissue-UIF-infect-bydep.csv** lists the maintenance cost (in terms of six metrics) of file_e, file_p1, and file_e_p1 for UIF anti-pattern.

**archissue-UHI-infect-bydep.csv** lists the maintenance cost (in terms of six metrics) of file_e, file_p1, and file_e_p1 for UHI anti-pattern.

**archissue-PKG-infect-bydep.csv** lists the maintenance cost (in terms of six metrics) of file_e, file_p1, and file_e_p1 for PKG anti-pattern.

**archissue-MVG-infect-bydep.csv** lists the maintenance cost (in terms of six metrics) of file_e, file_p1, and file_e_p1 for MVG anti-pattern.

**anchissue-filesize-byissue-bydep.csv** lists the file size (Loc percentage) of different affected files for each anti-pattern.

**casestudy-standard** folder contains the case study of architecture anti-patterns detected in Django project, and the motivation example in Section Introduction of our paper draft.


## 4. dependencies_from_stubs

This folder contains the data for several projects and the corresponding stub projects. The stub projects contains Python code with type annotations.

1)**projects-with-stubs.csv**

It lists the projects which have stub files. 
The code URLs, Stub URL, and versions are also provided.

2)**stub-deps**

Each subfolder corresponds to one project, including:
 
$*-P1.json$ contains the $P_1$ possible dependencies extracted from the methods in ASE work.

$*-stub-P1.json$ contains the $P_1$ possible dependencies extracted from the stub files.

3)**dependency-summary.csv**

This file illustrates the dependency extraction results, comparing ASE (our conference work) method (see (D(ase)) vs. the updated method (see D(ase+stub)).


## 5. dependency_verification
This folder contains the dataset of possible dependency verification.

The benchmarks were collected from execution traces by running testcases. We used *monkeytype* to monitor four projects (i.e., docutils, glance, pythonpattern, pythonvisitor) and used python *trace* to monitor the other four projects (i.e., algorithms, mimesis, mypy, and pygorithm).   


## Please reference our paper when you use this dataset.

    @inproceedings{2020ase-jin,
        title={Exploring the Architectural Impact of Possible Dependencies in Python Software},
		
        author={Jin, Wuxia and Cai, Yuanfang and Kazman, Rick and Zhang, Gang and Zheng, Qinghua and Liu, Ting},
        booktitle={2020 35th IEEE/ACM International Conference on Automated Software Engineering (ASE)},
        pages={1--13},
        year={2020},
        organization={IEEE}
        }

    @inproceedings{2019icse-jin,
      title={ENRE: a tool framework for extensible eNtity relation extraction},
	  
      author={Jin, Wuxia and Cai, Yuanfang and Kazman, Rick and Zheng, Qinghua and Cui, Di and Liu, Ting},
      booktitle={Proceedings of the 41st International Conference on Software Engineering: Companion Proceedings},
      pages={67--70},
      year={2019},
      organization={IEEE Press}
    }

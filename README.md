# Title-Insurance-Pipeline-Dashboard

**Goal:**
- Title Company wants a view of the outstanding pipeline of files to be completed by the Closing, Recording, and Policy Team.

**SOLUTION:** 
- Used SSIS/MS Server Agent to automatically filter data from the Operational Data Table to 3 Separate Tables (Closing_Workflow, Recording_Workflow, and Policy_Workflow) every hour.
- Created 3 Tableau Dashboards to visualize the outstanding files to be completed by each team.
- **Here is the Tableau Dashboards for [Title Insurance Pipeline](https://public.tableau.com/views/TitleInsurancePipelineDashboard/RecordingDashboard?:language=en-US&:display_count=n&:origin=viz_share_link)**

**SKILLS USED:** 
- **ChatGPT** to create the fictional dataset. 
- **SSIS** to filter data from the Operational Data to three separate tables for each team (Closing_Workflow, Recording_Workflow, and Policy_Workflow).
- **Tableau** for Visualizing the outstanding work to be completed.

**QUESTIONS ASKED:** 
- What kind of data would the managers of each team (Closing, Recording, and Policy) like to see at the top of the Dashboard?
- How can we automate the SSIS so the data from the warehouse goes into each of the teams' tables every hour?
                 
**PROCESS:**
1. Created a fictional Operational Data set in ChatGPT with the following columns: Transaction ID,	Transaction State,	Transaction Type,	Underwriter,	Client,	File Status,	Closing Date,	Recording Date, Policy Created Date. ***Assume the "Operational Data" is data taken from the title company's software they use to complete transactions.**
2. Created a Package in SSIS that would Filter rows by "File Status" column from the "Operational Data" and send it to 3 separate tables for each of the following teams: Closing Team, Recording Team, and Policy Team. This was mainly completed using the Conditional Split in SSIS (See screenshots below). 
![image](https://user-images.githubusercontent.com/96438722/230170108-468b2bf1-354f-44fa-b41a-db61f301a441.png)![image](https://user-images.githubusercontent.com/96438722/230170374-d766a2e2-5d7f-442e-93a5-41288a0f6ec0.png)
3. Once the SSIS Package was completed, a MS Server Agent schedule was created so that the SSIS Package would run every hour. So if any new data from the software updated in the Operational Data, that new row of data would be filtered to the appropriate team that needs to work on the file.
4. Now that we are done with the SSIS package, we can now connect the 3 database tables (Closing_Workflow, Recording_Workflow, and Policy_Workflow) and the Operational Data to Tableau. Whatever new data is populated into those tables during the MS Server Agent Schedule will automatically update in the appropriate team's Tableau Dashboard as well. This allows the teams to have a constant flow of new work going into their pipeline without having to manually retrieve it themselves.
5. Once the tables were connected to Tableau, I created a Dashboard for each team so they can pull their Daily/Hourly work. I also added some insights at the top of each of the Dashboards that would be important to managers.



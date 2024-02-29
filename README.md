<body>
    <h1>Healthcare</h1>
    <div style="text-align: center;">
        <img src="https://dsrichard97.github.io/Medicare/images2.png" width="300" height="250" />
        <img src="https://dsrichard97.github.io/Medicare/medi.jpeg" width="300" height="250" />
    </div>
    <div style="text-align: center;">
        <img src="https://img.shields.io/badge/Python_Version-3.10%2B-blue" alt="Python Version">
        <img src="https://img.shields.io/badge/SQL%2B-blue" alt="Google BigQuery">
        <img src="https://img.shields.io/github/last-commit/dsrichard97/Medicare_Dual_Enroll" alt="Last Commit">
        <img src="https://img.shields.io/badge/STAT-Causal_Inference-blue" alt="Causal Inference">
    </div>
    <p style="text-align: center;">Badge <a href="https://shields.io/">Source</a></p>
    <div>
        <h2>Authors</h2>
        <ul>
            <li><a href="https://github.com/dsrichard97">@dsrichard97</a></li>
        </ul>
    </div>
    <h2>Table of Contents</h2>
    <ul>
        <li><a href="#business-problem">Business Problem</a></li>
        <li><a href="#sql-code">SQL Code</a></li>
        <li><a href="#data-source">Data Source</a></li>
        <li><a href="#methods">Methods</a></li>
        <li><a href="#tech-stack">Tech Stack</a></li>
        <li><a href="#results">Quick Glance at the Results</a></li>
        <li><a href="#lessons">Lessons learned and Recommendation</a></li>
        <li><a href="#resources">Resources</a></li>
    </ul>
    <h2 id="business-problem">Business Problem</h2>
    <p> <strong>Context in the Healthcare Sector:</strong> This project evaluates the effectiveness of a wellness program in reducing healthcare utilization among Medicare and Medicaid dual enrollees, aiming to improve patient health outcomes and decrease costs. It seeks to provide a detailed analysis of dual enrollees through a causal inference approach, delivering insights for businesses to refine marketing and retention strategies.
    </p>
    <p>
        <strong>Business Challenge:</strong> Conduct data snooping to investigate possible models to use.
    </p>
    <h2 id="data-source">Data Source</h2>
    <p>
        <strong>Data Origin and Regulatory Background:</strong> The data for this project is derived from submissions made by states to the Centers for Medicare & Medicaid Services (CMS), as required under the Medicare Modernization Act (MMA). These submissions are stored in the form of monthly data on individuals enrolled in both Medicare and Medicaid (Dual Enrollees).
    </p>
    <h2 id="sql-code">SQL Code</h2>
    <pre><code>
WITH CleanedData AS (
    SELECT 
        State_Abbr,
        County_Name,
        Date,
        COALESCE(QMB_Only, 0) AS Total_QMB_Only, --using COALESCE to fill with 0 for null values
        COALESCE(QMB_plus_Full, 0) AS Total_QMB_plus_Full,
        COALESCE(SLMB_only, 0) AS Total_SLMB_only,
        COALESCE(SLMB_plus_Full, 0) AS Total_SLMB_plus_Full,
        COALESCE(QDWI, 0) AS Total_QDWI,
        COALESCE(QI, 0) AS Total_QI,
        COALESCE(Other_full, 0) AS Total_Other_full,
        COALESCE(Public_Total, 0) AS Total_Public_Total
    FROM 
`bigquery-public-data.sdoh_cms_dual_eligible_enrollment.dual_eligible_enrollment_by_county_and_program`
)
SELECT
    State_Abbr,
    County_Name,
    Date,
    SUM(Total_QMB_Only) AS Total_QMB_Only,
    SUM(Total_QMB_plus_Full) AS Total_QMB_plus_Full,
    SUM(Total_SLMB_only) AS Total_SLMB_only,
    SUM(Total_SLMB_plus_Full) AS Total_SLMB_plus_Full,
    SUM(Total_QDWI) AS Total_QDWI,
    SUM(Total_QI) AS Total_QI,
    SUM(Total_Other_full) AS Total_Other_full,
    SUM(Total_Public_Total) AS Total_Public_Total
FROM
    CleanedData
GROUP BY
    State_Abbr,
    County_Name,
    Date
ORDER BY
    State_Abbr,
    County_Name,
    Date;
    </code></pre>
    <p>From the previous code we can generate a sample data: <a href="https://github.com/dsrichard97/Medicare_Dual_Enroll/blob/main/dual.csv">Click here for data</a>.</p>
    <h2 id="methods">Methods - Causal inference (Initial Snooping)</h2>
    <ul>
        <li>Business Problem</li>
        <li>SQL Code</li>
        <li>Initial EDA</li>
        <li>Tableau Dashboard</li>
        <li>PowerPoint</li>
    </ul>
    <h2 id="tech-stack">Tech Stack</h2>
    <ul>
        <li>Google Cloud (Google BigQuery)</li>
        <li>Python</li>
        <li>Tableau</li>
    </ul>
    <ul>
        <li>
            <strong>Enrollments Over Time for Each Measure</strong>
            <br>
            This section provides a visual representation of enrollments over time for various measures.
            <br>
            <img src="https://dsrichard97.github.io/Medicare/graphs.png" srcset="https://dsrichard97.github.io/Medicare/graphs_medium.jpg 1000w, https://dsrichard97.github.io/Medicare/graphs_large.jpg 2000w" alt="Enrollments over time for each measure">
        </li>
        <li>
            <strong>Top 10 Counties</strong>
            <br>
            Highlights the top 10 counties based on specific criteria.
            <br>
            <img src="https://dsrichard97.github.io/Medicare/barchart.png" srcset="https://dsrichard97.github.io/Medicare/barchart_medium.jpg 1000w, https://dsrichard97.github.io/Medicare/barchart_large.jpg 2000w" alt="Top 10 counties based on specific criteria">
        </li>
        <li>
            <strong>Distributions</strong>
            <br>
            Showcases the distribution of data across different categories.
            <br>
            <img src="https://dsrichard97.github.io/Medicare/distrib.png" srcset="https://dsrichard97.github.io/Medicare/distrib_medium.jpg 1000w, https://dsrichard97.github.io/Medicare/distrib_large.jpg 2000w" alt="Distribution of data across different categories">
        </li>
        <li>
            <strong>Tableau Visuals</strong>
            <br>
            Presents Tableau visuals that offer insights into the data.
            <br>
            <img src="https://dsrichard97.github.io/Medicare/tab.jpeg" srcset="https://dsrichard97.github.io/Medicare/tab_medium.jpg 1000w, https://dsrichard97.github.io/Medicare/tab_large.jpg 2000w" alt="Tableau visuals showcasing data insights">
        </li>
    </ul>
    <p>To Visit Link: <a href="https://public.tableau.com/views/MEDICARE_17047605414730/Medicare?:language=en-US&:sid=&:display_count=n&:origin=viz_share_link">TABLEAU</a></p>
    <h2 id="lessons">Lessons</h2>
    <img src="https://dsrichard97.github.io/Medicare/comm.png" srcset="https://dsrichard97.github.io/Medicare/medium.jpg 1000w, https://dsrichard97.github.io/Medicare/large.jpg 2000w" alt="example" />
    <p>In addressing the business challenge to evaluate the effectiveness of a wellness program for Medicare and Medicaid dual enrollees, our data snooping efforts have yielded insightful results. By examining enrollment trends for 'SLMB Only', 'QMB Only', and 'QI' within Jefferson County, we observed distinct patterns that suggest a significant impact of the wellness program on healthcare utilization. With 'QI' enrollments relatively stable around 9,000, 'SLMB Only' close to 5,000, and 'QI' again near 3,000, the data points towards a varying degree of engagement across different segments of the dual enrollee population. These findings, set against the backdrop of Jefferson County's diverse demographic and healthcare landscape, underline the potential of targeted wellness programs to not only enhance patient health outcomes but also to strategically reduce costs. The distinct enrollment numbers across programs highlight areas where the wellness initiative is either thriving or requires further adaptation to meet enrollee needs more effectively. This analysis provides a foundation for businesses to refine marketing and retention strategies, focusing on personalized approaches to maximize the wellness program's impact on dual enrollees' <b>health management</b> and <b>cost containment</b>.
Further analysis reveals a noteworthy predominance of Qualified Medicare Beneficiaries (Full Medicaid Enrollees) within our data, particularly from 2015 to 2019, with Jefferson, Mobile, and Montgomery counties emerging as the top three contributors in the United States. Specifically, in Jefferson County, we find that 'QMB Only' enrollees represent the majority, followed by 'SLMB Only' enrollees, and then 'QI' enrollments. This pattern underscores the critical role these counties play in the broader context of healthcare utilization among dual enrollees. The success of our exploratory data analysis (EDA) in providing targeted insights into this specific group paves the way for further investigation through temporal trends, demographic analysis, and geographical distribution models. Such focused analyses promise to deepen our understanding of enrollment behaviors and the wellness program's effectiveness, offering valuable perspectives for tailoring future health initiatives and business strategies.</p>

 <h3 id="lessons">Lessons</h3>
 The exploration of data, despite its inherent complexities, underscores the crucial role of a skilled team in translating insights into actionable outcomes. Engaging in exploratory data analysis (EDA) has highlighted the power of visual storytelling and strategic reporting in uncovering hidden patterns and informing decision-making processes. However, the pursuit of further data-driven inquiries must align with the overarching goal of fostering business growth and providing actionable solutions. As a statistician, it is imperative to combine analytical expertise with effective communication to create compelling results for team or client. In summary, it is equally as important to be a domain expert.
    
    <h2 id="resources">Resources</h2>
    <ul>
        <li><a href="https://csulb-my.sharepoint.com/:p:/g/personal/richard_diazdeleon01_student_csulb_edu/EYy-nyChep5EqCPcvolVEsgBXFeoiqrH0wkjYPoxnf7QZA?e=k2u6kt">PowerPoint</a></li>
        <li><a href="https://public.tableau.com/views/MEDICARE_17047605414730/Medicare?:language=en-US&:sid=&:display_count=n&:origin=viz_share_link">TABLEAU</a></li>
        <li><a href="https://github.com/dsrichard97/Medicare_Dual_Enroll/blob/main/Healthcare_EDA.ipynb">Healthcare EDA notebook</a></li>
        <li><a href="https://github.com/dsrichard97/Medicare_Dual_Enroll/blob/main/hleveldualenroll.vsdx">High Level Overview</a></li>
    </ul>
</body>
</html>


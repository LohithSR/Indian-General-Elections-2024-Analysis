# Indian General Elections 2024 - Result Analysis

📊 **A Data-Driven Analysis of the Indian General Elections 2024 using SQL and DAX.**

## 📝 Project Overview
This project aims to analyze the results of the **Indian General Elections 2024** using **SQL-based data analysis**. The project leverages **Microsoft SQL Server** to extract, analyze, and visualize crucial election insights, including:
- 🏛️ **Seat Distribution** across states.
- 📊 **Party Performance** analysis.
- 🔍 **Candidate Statistics** (Votes, Victory Margins, and Performance).
- 📈 **EVM vs Postal Vote Breakdown**.
- 🗺️ **State-wise Political Trends**.

By utilizing structured queries and database relationships, this project provides **data-driven insights** into the **political landscape of India in 2024**.

---

## 🚀 Key Features
- **📌 Total Seats Per State** - Query to get seat distribution across all states.
- **📌 Winning Party Analysis** - Breakdown of seats won by NDA, I.N.D.I.A, and Others.
- **📌 Candidate-wise Results** - Winning candidates, their votes, party, and margin.
- **📌 Best Performing Political Parties** - Ranking of parties based on total seats won.
- **📌 Vote Type Distribution** - EVM vs Postal votes for candidates.
- **📌 Andhra Pradesh Special Report** - Deep dive into AP’s seat distribution, votes, and candidates.

---

## 🛠 Technologies Used
✅ **SQL Server** - For data extraction and analysis.
✅ **DAX Queries** - To enhance analytical insights.
✅ **ETL & Data Analysis** - Processing election data efficiently.
✅ **Power BI (Optional)** - For potential visual representations.

---

## 📂 Project Files
| File Name                                      | Description                                       |
|----------------------------------------------|-------------------------------------------------|
| `Copy of Purple and White Professional Science Project Presentation.pdf` | Project overview, results, and insights. |
| `election_analysis_queries.sql`              | SQL queries used for the election analysis.     |
| `README.md`                                  | This document describing the project.           |

---

## 🔍 SQL Queries Overview

### 📌 **1. Total Seats Available in Each State**
```sql
SELECT 
    s.State AS State_Name,
    COUNT(cr.Constituency_ID) AS Total_Seats_Available
FROM 
    constituencywise_results cr
JOIN 
    statewise_results sr ON cr.Parliament_Constituency = sr.Parliament_Constituency
JOIN 
    states s ON sr.State_ID = s.State_ID
GROUP BY 
    s.State
ORDER BY 
    s.State;
```

### 📌 **2. Seats Won by Major Alliances (NDA, I.N.D.I.A, Others)**
```sql
SELECT 
    SUM(CASE 
            WHEN party IN (
                'Bharatiya Janata Party - BJP', 
                'Telugu Desam - TDP', 
                'Janata Dal (United) - JD(U)',
                'Shiv Sena - SHS', 
                'AJSU Party - AJSUP', 
                'Apna Dal (Soneylal) - ADAL', 
                'Asom Gana Parishad - AGP',
                'Hindustani Awam Morcha (Secular) - HAMS', 
                'Janasena Party - JnP', 
                'Janata Dal (Secular) - JD(S)',
                'Lok Janshakti Party(Ram Vilas) - LJPRV', 
                'Nationalist Congress Party - NCP',
                'Rashtriya Lok Dal - RLD', 
                'Sikkim Krantikari Morcha - SKM'
            ) THEN [Won]
            ELSE 0 
        END) AS NDA_Total_Seats_Won
FROM 
    partywise_results;
```

### 📌 **3. Winning Candidate Details for a Specific State and Constituency**
```sql
SELECT cr.Winning_Candidate, p.Party, p.party_alliance, cr.Total_Votes, cr.Margin, cr.Constituency_Name, s.State
FROM constituencywise_results cr
JOIN partywise_results p ON cr.Party_ID = p.Party_ID
JOIN statewise_results sr ON cr.Parliament_Constituency = sr.Parliament_Constituency
JOIN states s ON sr.State_ID = s.State_ID
WHERE s.State = 'Uttar Pradesh' AND cr.Constituency_Name = 'AMETHI';
```

### 📌 **4. Best Performing Political Parties in Terms of Seats Won**
```sql
SELECT 
    p.party_alliance,
    COUNT(cr.Constituency_ID) AS Seats_Won
FROM 
    constituencywise_results cr
JOIN 
    partywise_results p ON cr.Party_ID = p.Party_ID
WHERE 
    p.party_alliance IN ('NDA', 'I.N.D.I.A', 'OTHER')
GROUP BY 
    p.party_alliance
ORDER BY 
    Seats_Won DESC;
```

### 📌 **5. Distribution of EVM Votes vs Postal Votes for Candidates**
```sql
SELECT 
    cd.Candidate,
    cd.Party,
    cd.EVM_Votes,
    cd.Postal_Votes,
    cd.Total_Votes,
    cr.Constituency_Name
FROM 
    constituencywise_details cd
JOIN 
    constituencywise_results cr ON cd.Constituency_ID = cr.Constituency_ID
WHERE 
    cr.Constituency_Name = 'MATHURA'
ORDER BY cd.Total_Votes DESC;
```

(*More queries can be found in the `election_analysis_queries.sql` file.*)

---

## 🏁 Conclusion
- The **NDA and I.N.D.I.A alliances** emerged as the dominant forces.
- **State-wise seat distribution** highlighted key regional trends.
- **Vote distribution analysis** showed the impact of EVM vs Postal votes.
- **Data Analytics played a crucial role** in understanding the election results.

---

## 🤝 Contributing
Want to improve this project?
1. **Fork the Repository**
2. **Create a Feature Branch** (`git checkout -b feature-name`)
3. **Commit Changes** (`git commit -m "Added new insights"`)
4. **Push to GitHub** (`git push origin feature-name`)
5. **Submit a Pull Request** 🚀

---

## 📬 Connect With Me
👤 **Lohith S R**  
📧 **Email**: lohithmagnate2004@gmail.com  
🔗 **LinkedIn**: [Lohith S R](https://www.linkedin.com/in/lohith-s-r)  
💻 **GitHub**: [LohithSR](https://github.com/LohithSR)  

📢 *Feel free to fork, contribute, and share your thoughts!* 🚀🔥


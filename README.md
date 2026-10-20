
# Find Your Study Spot

## Title & Team Information

**Project Title:** Find Your Study Spot

**Team Members:**
- Tiange Zhao - ashkeyz@uw.edu
- Ethan Wang - yuzew924@uw.edu
- Shengyuan Guo - sg243@uw.edu

**Track:** Product

**GitHub Repository:** https://github.com/ashkeyz-dev/search-rec-system.git

## Motivation & Problem Statement

Finding a suitable study space on UW's Seattle campus can require checking several university webpages for information about noise levels, outlets, seating, and opening hours. This process takes time and students may still struggle to determine which space best fits their activities and preferences. We aim to build a search and recommendation system that brings this information together and helps students identify suitable study spots for a particular visit.

For example, four classmates meeting from 6 to 8 p.m. might need outlets and a place where they can talk, while having a whiteboard would be a bonus. Excluding every space without a whiteboard could leave out good options, but suggesting a room that closes at 7 p.m. would not help either. Our system will let students separate what they need from what they would prefer, then rank suitable spaces based on their search and preferences. We will compare this approach with keyword search and filters alone to see whether it brings more useful options to the top.

## Background & Related Work

UW previously designed an application called SpaceScout that can help students find study spaces by noise level, opening hours, capacity, outlets, and other features (Hickey). However, these resources mainly organize spaces by library or reservation category rather than ranking them based on students' combined preferences. We can build on this idea by supporting natural-language queries, cross-location search, and personalized recommendations. Rather than relying only on filters, we aim to rank study spaces based on how well they match a student's specific needs and preferences.

Cha and Kim surveyed 252 students to understand their preferences for study environments. Important factors included noise level, crowdedness, available space, furniture comfort, and cleanliness. These findings highlight that students consider multiple factors when choosing a study space, and different students may prioritize these factors differently. Our project will use these findings to guide the selection of study-space attributes and develop a preference-based ranking system that allows students to find spaces that better match their individual needs.

## Proposed Approach and System Design

**Data Collection:** We will collect information about around 30 study areas across UW campus. Our sources will include UW Libraries pages and official room reservation pages. We will also visit selected spaces to check missing details. Each record will include the location, opening hours, capacity, average noise level, study environment, and available equipment. We will save the source and the date we checked. Missing details will be marked as "unknown."

**Key Components:** The system will consist of a study space database, a search index, a ranking module, and a web interface. We will preprocess the description of study space by tokenizing it into words and normalizing text. Each study area will be one document, and an inverted index will connect search terms to matching spaces. Users will be able to enter natural-language queries and select filters based on their study needs.

**Search and Ranking:** We will use BM25 as our baseline retrieval algorithm to score how well each study-space description matches the user's query, building on the TF-IDF and best-match ranking methods. Users can mark features as either required or preferred. For example, they may require power outlets but only prefer a whiteboard. The system will first filter out spaces that do not meet required conditions, including opening hours for the intended visit. Unknown details will not count as confirmed matches. The remaining spaces will then be ranked using a combination of normalized BM25 score and weighted preference matches. This allows the system to consider both textual relevance and individual study needs.

**Evaluation:** We will compare three versions: (1) BM25 keyword search alone, (2) BM25 with requirement filtering, and (3) BM25 with filtering and preference ranking. We will also consider TF-IDF as a simpler retrieval baseline. We will create realistic search scenarios with different study requirements and evaluate the ranked results using NDCG@5, which measures how well highly relevant results appear near the top. We will also check whether the results satisfy users' required conditions. If time allows, we will experiment with sentence embeddings and cosine similarity to see whether semantic matching improves results for queries such as "a place to focus" and "quiet study."

**Expected Outputs:** The website will show a ranked list of recommended study spaces with explanations of which needs and preferences each meets. Each result will also show unknown details, source links, and update dates. The first version will use published hours and checked facilities rather than live noise levels or occupancy.

## Project Timeline & Milestones

| Week | Milestone | Expected Output |
|------|-----------|-----------------|
| 4 | Finish the proposal. Agree on the project scope and team roles. | Project plan and task list |
| 5 | Collect data for around 30 study areas. Check missing details and record sources. | Clean dataset |
| 6 | Process the text and build an inverted index. Set up BM25 search. | Working keyword search |
| 7 | Add filters for required conditions. Build preference scores and combine them with BM25 scores. | Search with filters and preference ranking |
| 8 | Finish the web interface. Prepare and label search queries. Keep separate sets for tuning and final testing. | Working website and labeled query sets |
| 9 | Compare the three search versions. Measure NDCG@5 and errors in meeting required conditions. Fix problems. | Results table, charts, and an updated system |
| 10 | Write the final report. Record the demo video and check all submission files. | Final report, video, and working demo |

## Roles and Responsibilities

All members will share responsibilities across the project, including data collection, modeling, evaluation, and report writing. Each member will have a primary focus while contributing to other areas:

- **Tiange Zhao:** Data collection and preparation, report writing.
-  Search and ranking algorithms, modeling, evaluation.
-  Website development, usability testing.

## References

1. Hickey, Hannah. "SpaceScout App Hunts for Study Spaces, and MyUW Goes Mobile for Students." *UW News*, 24 Oct. 2012.  
   https://www.washington.edu/news/2012/10/24/spacescout-app-hunts-for-study-spaces-and-myuw-goes-mobile-for-students/

2. Cha, Seung Hyun, and Tae Woo Kim. "What Matters for Students' Use of Physical Library Space?" *The Journal of Academic Librarianship*, vol. 41, no. 3, 2015.  
   https://doi.org/10.1016/j.acalib.2015.03.014

3. University of Washington Libraries. (n.d.). *Study Spaces*.  
   https://lib.uw.edu/locations-hours/spaces-technology/study-spaces/

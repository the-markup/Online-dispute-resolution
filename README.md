# Data and Methodology for: Payday Lenders Are Big Winners in Utah’s Chatroom Justice Program

This contains the data and methodology for our story "[Payday Lenders Are Big Winners in Utah’s Chatroom Justice Program](https://themarkup.org/zoom-justice/2022/03/16/payday-lenders-are-big-winners-in-utahs-chatroom-justice-program/)."

## Methodology
Utah launched its online dispute resolution (ODR) system on Sept. 18, 2018, as a pilot project for small claims cases—those in which the amount in question is less than $11,000—in West Valley City Justice Court.

Since then, the program has expanded to dozens of courts across the state, and Utah Courts officials hope that all small claims cases will go through the ODR process by the end of this year. 

In all courts that use ODR, the process is mandatory, and if the defendant fails to register for the ODR system within 14 days, the court can issue a default judgment against them. These rulings are often followed by writs of garnishment allowing the plaintiff to garnish some of the defendants wages until the debt is repaid.

High rates of default judgments are seen as a weakness in the judicial system—evidence that many litigants are either unable or unwilling to participate in the process.

One of the primary goals of Utah’s ODR project is to reduce the rate of default judgments. To examine the effect ODR has had on the state, we set out to measure how the default judgment rate changed after the system was introduced.

Through public records requests, we obtained two datasets from Utah Courts. 

The first—the pre-ODR dataset—encompassed all small claims cases filed across all courts in the state from Sept. 18, 2016, through Sept. 18, 2018, the two years before the launch of the ODR system. The second—the ODR dataset—covered all cases filed from Sept. 19, 2018, through Feb. 2, 2022, in courts that used the ODR system.

Because we were only concerned with the ultimate outcome of cases, we removed all pending cases—those without a listed disposition—from both datasets.

Cases that result in default judgments often reach their resolution faster than cases that go to trial or result in other kinds of dispositions. Because our ODR dataset, which included cases filed as recently as Feb. 2, 2022, was much more recent than the pre-ODR dataset, we were concerned that it would skew more heavily toward default judgments—as more pending cases are resolved, it’s more likely that they will result in a disposition other than a default judgment. We know this simply because it’s taken those cases longer to resolve.

To avoid that problem, we restricted our ODR dataset to cases filed by Jan. 31, 2021, which significantly reduced the number of cases pending disposition.

That meant we were left with only three courts—West Valley City Justice Court, Orem City Justice Court, and Carbon County Justice Court—that appeared in both the pre-ODR and ODR dataset because many courts started using the ODR system after January 2021.

The pre-ODR dataset contained a number of cases listed as “small claims government” cases. The ODR dataset did not differentiate between normal small claims cases and small claims government cases. According to Utah Courts officials, one court in the state—Carbon County Justice Court—processes some of its small claims government cases through the ODR system. However, the pre-ODR dataset we obtained did not contain enough information to determine which small claims government cases out of Carbon County would have qualified for ODR. To work around that barrier, we removed all small claims government cases from our dataset and limited our analysis to courts with reliable pre- and post-ODR data.

This left us with pre-ODR and ODR data for two courts: West Valley City Justice Court and Orem City Justice Court.

Next, we cleaned the data to ensure that plaintiff names were uniform (making sure that “Money4You,” “Mony 4 You,” and “Money for You” were all properly named “Money 4 You,” for example).

We then created a custom ID for each case by combining the original case number assigned by the court with the name of the court. For example, case 228900045 out of Orem City Justice Court received the custom ID “228900045Orem City Justice Court.” 

We did this because different courts in Utah sometimes use the same case number for separate cases. For example, there may be a case 228900045 in Orem City Justice Court and a case 228900045 in West Valley City Justice Court.

Next, we coded all cases with dispositions recorded as “jdmt default judge” and “jdmt default clerk” as “Default Judgment” and cases with any other kind of disposition as “Other.”

We wanted to analyze the difference between cases brought by frequent plaintiffs—often businesses, who we termed “institutional plaintiffs”—and those brought by individual plaintiffs.

To do this, we followed the strategy employed by the National Center for State Courts in its 2020 study of Utah’s ODR system. Individual plaintiffs were classified as those that had a first and last name recorded, while institutional plaintiffs were those for which only a last name was recorded. In Utah’s court record system, business names are listed under the last name field. We created a new column and labeled plaintiffs as either “institutional plaintiff” or “individual plaintiff.”

Finally, we combined the pre-ODR and ODR datasets and added an extra column in which we labeled whether the case was “pre-ODR” or “ODR.”

To determine the change in default judgment rates, we performed a pivot table analysis on the West Valley City Justice Court and Orem City Justice Court data, where the pre-ODR/ODR designations were the rows, the disposition categories were the columns, and values were unique counts of our custom ID. This ensured that we only counted each case once. 

To determine which entities filed the most cases, we performed another pivot table analysis using plaintiff last names as the rows and unique count of our custom ID as the values.

To determine the difference in default rates between cases brought by institutional and individual plaintiffs, we performed a pivot table analysis on the combined pre-ODR and ODR datasets where the plaintiff designations were the rows, the disposition categories were the columns, and the values were unique counts of our custom ID.

A note of caution for anyone who wants to use the original, statewide datasets we obtained from Utah Courts: There may be some discrepancies in how different courts record dispositions. Most notably, Ogden Justice Court—which had the second most small claims cases in the state—did not record a single case as ending in a default judgment. Instead, it appears, those cases were simply recorded as ending in “judgment.”

**Another note about the data:**

Utah Courts officials told The Markup that a relatively large percentage of the cases in both datasets with dispositions of “dismissed without prejudice” represent cases in which the defendant was never successfully served with the lawsuit. When Utah conducts its own analyses of default rates, it excludes cases in which the defendant wasn’t successfully served because those cases never actually began for all intents and purposes. 

The datasets we received did not contain the data field required to determine whether a case was dismissed without prejudice because service was unsuccessful or for some other reason. As a result, we kept all cases dismissed without prejudice in our datasets and they were included in the total number of cases against which we calculated default judgment rates..

This limitation does not affect the overall trend we documented of a rise in default judgments because we kept cases dismissed without prejudice in both datasets. But the default judgment rates published by Utah Courts—both before and after ODR—will likely be higher than those we calculated because they removed cases that were dismissed without prejudice due to a failure to serve from their datasets.

## Data dictionary
### Utah_ODR_pre.csv

This file contains disposition data for all cases filed in Utah small claims courts from September 18, 2016 through September 18, 2018.

[Utah_ODR_pre.csv](https://github.com/the-markup/Online-dispute-resolution/blob/main/Utah_ODR_pre.csv?raw=true) - 1.66 MB. 16,808 rows. First row is the header (CSV).

<table border="0" class="dataframe">
  <thead>
    <tr style="text-align: left;">
      <th>Column</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
  <tr><td>int_case_num</td><td>An case number assigned by Utah Courts for internal tracking purposes </td></tr>
<tr><td>case_num</td><td>The public identification number assigned to each case. Different courts may assign the same case number to separate cases</td></tr>
<tr><td>filing_date</td><td>The date the case was filed with the court</td></tr>
<tr><td>case_type</td><td>An abbreviation of the case type description</td></tr>
<tr><td>case type descr</td><td>A description of the case type (e.g., small claims, small claims - government, etc.)</td></tr>
<tr><td>locn_descr</td><td>The court where the case is located</td></tr>
<tr><td>disp_date</td><td>The date the case was disposed</td></tr>
<tr><td>disp_code</td><td>An abbreviation of the disposition description</td></tr>
<tr><td>disp_descr</td><td>A description of the case’s disposition (e.g., default judgment, dismissed with prejudice, trial, etc.)</td></tr>
<tr><td>party_code</td><td>	Designation of whether the party was a plaintiff or defendant in the case</td></tr>
<tr><td>last_name</td><td>The party’s last name</td></tr>
<tr><td>first_name</td><td>The party’s first name</td></tr>
  </tbody>
</table>

### Utah_ODR_post.csv

This file contains disposition data for all cases filed through the online dispute resolution system in Utah small claims courts, beginning September 19, 2018, when the pilot program launched in West Valley City Justice Court.

[Utah_ODR_post.csv](https://github.com/the-markup/Online-dispute-resolution/blob/main/Utah_ODR_post.csv?raw=true) - 14.7 MB. 114,208 rows. First row is the header (CSV).

<table border="0" class="dataframe">
  <thead>
    <tr style="text-align: left;">
      <th>Column</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
<tr><td>case_num</td><td>The public identification number assigned to each case. Different courts may assign the same case number to separate cases</td></tr>
<tr><td>filing_date</td><td>The date the case was filed with the court</td></tr>
<tr><td>locn_desc</td><td>The court where the case is located</td></tr>
<tr><td>disp_descr</td><td>A description of the case’s disposition (e.g., default judgment, dismissed with prejudice, trial, etc.)</td></tr>
<tr><td>disp_date</td><td>The date the case was disposed</td></tr>
<tr><td>party_type_description</td><td>Designation of whether the party was a petitioner (plaintiff) or respondent (defendant) in the case</td></tr>
<tr><td>last_name</td><td>The party’s last name</td></tr>
<tr><td>first_name</td><td>The party’s first name</td></tr>
  </tbody>
</table>

Questions? Write to us: [todd.feathers@themarkup.org](mailto:todd.feathers@themarkup.org) 
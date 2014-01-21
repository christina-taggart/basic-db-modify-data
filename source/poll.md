CREATE TABLE congress_members (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  name VARCHAR(64) NOT NULL,
  party VARCHAR(64) NOT NULL,
  location VARCHAR(64) NOT NULL,
  grade_1996 REAL,
  grade_current REAL,
  years_in_congress INTEGER,
  dw1_score REAL
, created_at DATETIME, updated_at DATETIME);
CREATE TABLE voters (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    first_name VARCHAR(64) NOT NULL,
    last_name  VARCHAR(64) NOT NULL,
    gender VARCHAR(64) NOT NULL,
    party VARCHAR(64) NOT NULL,
    party_duration INTEGER,
    age INTEGER,
    married INTEGER,
    children_count INTEGER,
    homeowner INTEGER,
    employed INTEGER,
    created_at DATETIME NOT NULL,
    updated_at DATETIME NOT NULL
  );
CREATE TABLE votes (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    voter_id INTEGER,
    politician_id INTEGER,
    created_at DATETIME NOT NULL,
    updated_at DATETIME NOT NULL,
    FOREIGN KEY(voter_id) REFERENCES voters(id),
    FOREIGN KEY(politician_id) REFERENCES congress_members(id)
  );

  delete from voters where voters.id in (select voters.id from voters
   ...> join votes on voters.id = voter_id
   ...> where party not in ('Republican','Democrat')
   ...> group by voters.id
   ...> having count(voter_id) < 2);

delete from voters where homeowner = 1 and employed = 1
   ...>   and children_count=0 and party_duration < 3 and id in (select voter_id from votes
   ...>   where politician_id in (select id from congress_members where grade_current > 12));

update votes set politician_id = 346 where voter_id in (select id from voters where age > 80 and children_count = 0);

update votes set politician_id = (select id from congress_members order by grade_1996 limit 1) where politician_id=(select id from congress_members order by grade_1996 desc limit 1);
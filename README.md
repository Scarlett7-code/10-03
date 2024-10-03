-- 35. Mennyi a váltószáma az aprópénznek azokban az országokban, ahol nem 100?
    SELECT valtopenz, orszag FROM orszagok WEHERE valtopenz != '%100%'
-- 36. Hány ország területe kisebb Magyarországénál?
    SELECT orszag, terulet FROM orszagok WEHERE terulet < (SELECT terulet FROM orszagok WHERE orszag LIKE 'MAGYARORSZÁG')
-- 37. Melyik a legnagyobb területű ország, és mennyi a területe?
    SELECT MAX(terulet), orszag FROM orszagok
-- 38. Melyik a legkisebb területű ország, és mennyi a területe?
    SELECT MIN(terulet), orszag FROM orszagok
-- 39. Melyik a legnépesebb ország, és hány lakosa van?
    SELECT MAX(nepesseg*1000) orszag FROM orszagok
-- 40. Melyik a legkisebb népességű ország, és hány lakosa van?
    SELECT MIN(nepesseg*1000) orszag FROM orszagok
-- 41. Melyik a legsűrűbben lakott ország, és mennyi a népsűrűsége?
    SELECT MAX(nepesseg*1000/terulet) orszag FROM orszagok
-- 42. Melyik a legritkábban lakott ország, és mennyi a népsűrűsége?
    SELECT MIN(nepesseg*1000/terulet) orszag FROM orszagok
-- 43. Melyik a legnagyobb afrikai ország és mekkora?
    SELECT MAX(terulet), orszag FROM orszagok WHERE foldr_hely LIKE '%AfrikaA%'
-- 44. Melyik a legkisebb amerikai ország és hányan lakják?
    SELECT MIN(terulet) orszag, nepesseg*1000 WHERE foldr_hely LIKE '%Amerika%'
-- 45. Melyik az első három legsűrűbben lakott "országméretű" ország (tehát nem város- vagy törpeállam)? Elvárt megoldás: MÁLTA, BANGLADES, MALDIV-SZIGETEK
   SELECT orszag FROM orszagok WHERE foldr_hely NOT LIKE '%város%' OR '%törpeállam%' ORDER BY nepesseg*1000/terulet LIMIT 3 
-- 46. Melyik a világ hat legnépesebb fővárosa?
    SELECT fovaros, orszag FROM orszagok ORDER BY nepesseg*1000 LIMIT 6
-- 47. Melyik tíz ország egy főre jutó GDP-je a legnagyobb?
    SELECT orszag, gdp FROM orszagok ORDER BY gdp/nepesseg*1000 LIMIT 10
-- 48. Melyik tíz ország össz-GDP-je a legnagyobb?
    SELECT orszag, gdp FROM orszagok ORDER BY gdp LIMIT 10
-- 49. Melyik országban a legszegényebbek az emberek (legkisebb a GDP, ahol egyáltalán van GDP)?
     SELECT orszag, gdp FROM orszagok ORDER BY gdp LIMIT 10 DESC
-- 50. Melyik a 40. legkisebb területű ország?
     SELECT orszag, terulet FROM orszagok ORDER BY terulet LIMIT 1 OFFSET 40 DESC;
-- 51. Melyik a 15. legkisebb népsűrűségű ország?
    SELECT orszag FROM orszagok ORDER BY nepesseg*1000/terulet LIMIT 1 OFFSET 14 DESC;
-- 52. Melyik a 61. legnagyobb népsűrűségű ország?
    SELECT orszag FROM orszagok ORDER BY nepesseg*1000/terulet LIMIT 1 OFFSET 60;
-- 53. Melyik három ország területe hasonlít leginkább Magyaroszág méretéhez?

-- 54. Az emberek hányadrésze él Ázsiában?
-- 55. A szárazföldek mekkora hányadát foglalja el Oroszország?
-- 56. Az emberek hány százaléka fizet euroval?
-- 57. Hányszorosa a leggazdagabb ország egy főre jutó GDP-je a legszegényebb ország egy főre jutó GDP-jének?
-- 58. A világ össz-GDP-jének hány százalékát adja az USA?

-- 59. A világ össz-GDP-jének hány százalékát adja az euroövezet?

-- 60. Melyek azok az átlagnál gazdagabb országok, amelyek nem az európai vagy az amerikai kontinensen találhatóak?

-- 61. Milyen államformák léteznek Európában?
    SELECT DISTINCT allamforma FROM orszagok WHERE foldr_hely LIKE '%Európa%'
-- 62. Hányféle államforma létezik a világon?
     SELECT DISTINCT COUNT(allamforma) FROM orszagok 
-- 63. Hányféle fizetőeszközt használnak Európában az eurón kívül?
    SELECT DISTINCT COUNT(penznem) FROM orszagok WHERE foldr_hely LIKE '%Európa%' AND penznem NOT LIKE '%euró%;
-- 64. Mely pénznemeket használják több országban is?
    SELECT penznem FROM orszagok GROUP BY penznem HAVING COUNT(*) > 1 

1. To alter a sp, simply run the Alter statement against the code.
```sql
ALTER PROCEDURE spFilmList AS
BEGIN
  SELECT
	 FilmName,
	 FilmReleaseDate,
	 FilmRunTimeMinutes
  FROM
     tblFilm
  ORDER BY
     FilmName ASC
END
```

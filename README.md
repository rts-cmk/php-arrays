# Arrays

## Hvad er et array?

> Et array er inden for programmering en betegnelse for en variabel der indeholder en række af værdier, associeret med en nøgle. Nøglen er typisk et heltal, men nogle programmeringssprog tillader brugen af strenge og andre datatyper til identificering og sortering

Eksempel:
```
[ nøgle => værdi, nøgle => værdi, ... ]
```

## Hvordan opretter man et array?

Alt efter situationen i din applikation, er der forskellige metoder til at oprette et array.

Nogle metoder opretter arrays for dig automatisk, andre kræver at du eksplicit definerer dit array.

```php
$myArray = ['username' => 'admin', 'password' => '1234'];
$myArray = array('username' => 'admin', 'password' => '1234');
```

> ### Øvelse 1
> Sammenlign outputtet fra de to ovenstående metoder til at oprette et array. Brug `print_r()` til at udskrive arrays.

## Tre forskellige typer af arrays
Et array kan være enten
* Indekseret,
* Associativt, eller
* Multidimensionelt

Forskellen mellem indekserede og associative arrays er, at nøglerne i et indekseret array er fortløbende tal (0, 1, 2, 3, ...), og i et associativt array er nøglerne navngivet som strenge ('user', 'password', 'name', ...).

> ### Øvelse 2
> Prøv at se hvad forskellen i outputtet af disse to arrays er:
```php
$myIndexedArray = ['admin', '1234'];
$myAssocArray = ['user' => 'admin', 'password' => '1234'];
```

Du kan også selv definere den indekserede nøgle i et array:

```php
$myArray = [0 => 'admin', 1 => '1234'];
// eller
$myArray[0] = 'admin';
$myArray[1] = '1234';
```

### Multidimensionelle arrays
Et multidimensionelt array er et array med et eller flere arrays.

Når et array optræder som en del af at overordnet array er det altid som værdien, aldrig som nøglen.

```php
$myArray = [
	'user' => 'admin',
	'phone' => [
		'12345678',
		'87654321',
		'54321678'
	]
];
```

## Sådan læser du et array

Der findes masser af forskellige måder at læse et array.

Den letteste er nok at bede om at få udskrevet værdien af hver enkelt nøgle direkte, en efter en:

```php
$myArray = ['æble', 'pære', 'banan', 'mango'];

echo $myArray[0]; // æble
echo $myArray[1]; // pære
echo $myArray[2]; // banan
echo $myArray[3]; // mango
```

Men dette er ikke særligt hensigtsmæssigt, eftersom vi som regel ikke kender længden af et array, eller ved hvilket indeks, der dækker over hvilke data.

Derfor kan vi benytte nogle metoder til at læse et array, for eksempel løkker. Dette kalder vi en iteration, eller at iterere.

```php
$myArray = ['æble', 'pære', 'banan', 'mango'];
$length = count($myArray);

for ($i = 0; $i < $length; $i++) {
	echo $myArray[$i];
}
```

Problemet med løkker er, at  de kan være ret process-tunge. Dvs. at de bruger rigtig meget hukommelse og processor-kraft. Løkker tager som regel lang tid for et program at udføre.

Som et alternativ findes der en række funktioner til at filtrere eller formatere et array: [`array_map`](http://php.net/manual/en/function.array-map.php), [`array_filter`](http://php.net/manual/en/function.array-filter.php) og [`array_walk`](http://php.net/manual/en/function.array-walk.php) for bare at nævne de mest almindelige.

`array_map` og `array_walk` gør næsten det samme. Begge funktioner returnerer et nyt array, hvor hvert enkelt element i det oprindelige array er formateret efter nogle regler du definerer.

```php
$myArray = ['username' => 'admin', 'password' => '1234'];

function formatArray($key, $value) {
	return '<p>' . $key . ': ' . $value . '</p>';
}

$newArray = array_map('formatArray', array_keys($myArray), $myArray);

echo implode('', $newArray);
```

`array_filter` bruges til at hente et eller flere elementer ud af et array. `array_filter` laver også et nyt array.

```php
$myArray = ['username' => 'admin', 'password' => '1234'];

function findUser($key) {
	return $key === 'username';
}

$user = array_filter($myArray, 'findUser', ARRAY_FILTER_USE_KEY);

echo implode('', $user);
```

> ### Øvelse 3
> Opret forbindelse til en database og hent noget data. Brug metoderne ovenfor til at bearbejde de arrays, der kommer ud af databasekaldende.

## Automatisk genererede arrays
Vi har kigget på hvordan vi selv kan oprette og definere arrays.

Men mange arrays i programmering bliver oprettet automatisk gennem en eller flere indbyggede funktioner.

Her er en liste over de typiske steder et automatisk genereret array kan komme fra:

* MySQL resultater (mysqli og PDO)
* $_POST
* $_GET
* $_SESSION
* $_COOKIE
* $_REQUEST
* $_SERVER
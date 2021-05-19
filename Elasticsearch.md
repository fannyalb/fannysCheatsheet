# Einfacher Watcher

## Schedule 

Wie oft der Watcher getriggert wird:
* `"interval" : "10m"` ... alle 10 Minuten
* `"hourly" : {"minute" : 30 }` ... jede Stunde um "halb" (0:30, 13:30, ...)
* `"daily" : { "at" : ["midnight", "noon", "17:00" ] }`
* `"cron" : "0 0 12 * * ?"` ... jeden Tag um 12h Mittag

```json
{
  "trigger": {
	"schedule": {
	  "interval": "10m"
	}
  }
```

##  Input

Holt die Daten, die wir evaluieren wollen.
* `"query" :  { "match_all" : {}}` ... keine Einschränkung, alle Logs
* `"query" : { "match" : { "prio.keyword" : "PRIO_INFO" }}` ... Nur Eintraege, wo
"PRIO_INFO" im Feld "prio.keyword" steht

```json
	"input": {
	  "search": {
		"request": {
		  "indices": [ "myindex*" ],
		  "body": {
			"query": {
			  "match": {
				"prio.keyword": "PRIO_INFO"
			  }
			}
		  }
		}
	  }
	},
	{
	  "trigger": {
		"schedule": {
		  "interval": "10m"
		}
	  },
	  "input": {
		"search": {
		  "request": {
			"search_type": "query_then_fetch",
			"indices": [
			  "myindex*"
			],
			"rest_total_hits_as_int": true,
			"body": {
			  "query": {
				"match": {
				  "prio.keyword": "PRIO_INFO"
				}
			  }
			}
		  }
		}
	  },
	  "condition": {
		"compare": {
		  "ctx.payload.hits.total": {
			"gte": 0
		  }
		}
	  },
	  "actions": {
		"send_email": {
		  "email": {
			"profile": "standard",
			"to": [
			  "your@mail.com"
			],
			"subject": "Watcher notification",
			"body": {
			  "text": "{{ctx.payload.hits.total}} PRIO_INFOS"
			}
		  }
		}
	  }
	}
```

## Filter

* **`"bool"`**: hier sind alle Bedingungen definiert, die in der Suche erfuellt sein
muessen
* Jede Bedingung hat eine "Auftrittsbedingung" (Vorkommensbedingung):
  * `"must"`: Bedingung muss erfuellt sein
	* `"filter"`: Bedingungen muessen erfuellt sein, Unterschied zu `must` nicht
		ganz klar
	* `"should"`: ?
	* `"must_not"`

### `"filter"`
* `"range"`: Fuer Intervalle (Zeit, Int, ...)

	```json
	{
	  "query": {
			"bool" : {
				"must": [
					{ "match" : { "prio.keyword" : "PRIO_ERROR" }}
				],
				"filter" : [
					"range" : {
						"@timestamp": {
							"gte" : "{{ctx.trigger.scheduled_time}}||-10m",
							"lte": "{{ctx.trigger.scheduled_time}}"
						}
						
					}

				]
		}

## Watcher-Context-Felder
* `{{ctx.trigger.scheduled_time}}`: Zeit, zu der der Trigger ausgeloest werden
	sollte
* `{{ctx.payload.hits.total}}`: Anzahl, der mittels Query gefundenen Resultate
* `{{ctx.watch_id}}`: UID des Watchers


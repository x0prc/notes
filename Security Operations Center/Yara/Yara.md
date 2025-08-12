---
{"dg-publish":true,"permalink":"/src/site/notes/src/site/notes/src/site/notes/src/site/notes/main/cs/security-operations-center/yara/yara/"}
---






- Used for threat hunting, forensics and intelligence.

```YAML
rule examplerule {
        condition: true
}
```

- Simply, the rule we have made checks to see if the file/directory/PID that we specify exists via `condition: true`.

```YAML
rule helloworld_checker{
	strings:
		$hello_world = "Hello World!"
}
```

- keyword `Strings` where the string that we want to search, i.e., "Hello World!" is stored within the variable `$hello_world` .

![Untitled 4.png|Untitled 4.png](/img/user/img/Untitled%204.png)

## Yara Tools

- LOKI is a free open-source IOC (_Indicator of Compromise_) scanner created/written by Florian Roth.
- THOR (superhero named programs for a superhero blue teamer)
- FENRIR
- YAYA (_Yet Another Yara Automation_)
- yarGen is a generator for YARA rules.
- Valhalla — _boosts your detection capabilities with the power of thousands of hand-crafted high-quality YARA rules._
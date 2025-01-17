require 'yaml'

require File.join(File.dirname(__FILE__), 'lib', 'github_repository_ripper')
require File.join(File.dirname(__FILE__), 'lib', 'github_commit_ripper')

LANGUAGES_TO_SEARCH = ['C', 'csharp', 'C%2B%2B', 'Java', 'JavaScript', 'Perl', 'PHP', 'Python', 'Ruby']

namespace :rip do

  desc "Rip all repositories"
  task :repositories do
    pages_to_rip = 1
    GitHubRepositoryRipper.rip_repositories(LANGUAGES_TO_SEARCH, pages_to_rip)
  end

  desc "Rip all commits"
  task :commits do
    repositories = YAML.load_file('repositories.yml')
    GitHubCommitRipper.rip_all_commits(repositories)
  end

  desc "Write all commits to one big file"
  task :merge_commits do
    all_commits = {}
    Dir.glob('commit*.yml').map do |file|
      puts file
      yaml = YAML.load_file(file)
      next unless yaml
      yaml.each do |commit|
        all_commits[commit[:language]] ||= []
        all_commits[commit[:language]] << commit
      end
    end

    all_commits.keys.each do |language|
      output_path = "language-commits[#{language}].yml"
      puts output_path
      File.delete(output_path) if File.exist?(output_path)
      File.open(output_path, 'w') do |file|
        messages = all_commits[language].map { |commit| { :message => commit[:message] } }
        file.puts(YAML.dump(messages))
      end
    end
  end

end

namespace :stats do

  desc "Shows all profanity in the messages"
  task :profanity do
    words = %w{
      a55
      a55hole
      aeolus
      ahole
      anal
      analprobe
      anilingus
      anus
      areola
      areole
      arian
      aryan
      ass
      assbang
      assbanged
      assbangs
      asses
      assfuck
      assfucker
      assh0le
      asshat
      assho1e
      ass hole
      assholes
      assmaster
      assmunch
      asswipe
      asswipes
      azazel
      azz
      b1tch
      babe
      babes
      ballsack
      bang
      banger
      barf
      bastard
      bastards
      bawdy
      beaner
      beardedclam
      beastiality
      beatch
      beater
      beaver
      beer
      beeyotch
      beotch
      biatch
      bigtits
      tits
      bimbo
      bitch
      bitched
      bitches
      bitchy
      blow
      blowjob
      blowjobs
      bod
      bodily
      boink
      bollock
      bollocks
      bollok
      bone
      boned
      boner
      boners
      bong
      boob
      boobies
      boobs
      booby
      booger
      bookie
      bootee
      bootie
      booty
      booze
      boozer
      boozy
      bosom
      bosomy
      bowel
      bowels
      bra
      brassiere
      breast
      breasts
      bugger
      bukkake
      bullshit
      bull shit
      bullshits
      bullshitted
      bullturds
      bung
      busty
      butt
      butt fuck
      buttfuck
      buttfucker
      buttfucker
      buttplug
      c.0.c.k
      c.o.c.k.
      c.u.n.t
      c0ck
      c-0-c-k
      caca
      cahone
      cameltoe
      carpetmuncher
      cawk
      cervix
      chinc
      chincs
      chink
      chink
      chode
      chodes
      cl1t
      climax
      clit
      clitoris
      clitorus
      clits
      clitty
      cocain
      cocaine
      cock
      c-o-c-k
      cockblock
      cockholster
      cockknocker
      cocks
      cocksmoker
      cocksucker
      cock sucker
      coital
      commie
      condom
      coon
      coons
      corksucker
      crabs
      crack
      cracker
      crackwhore
      crap
      crappy
      cum
      cummin
      cumming
      cumshot
      cumshots
      cumslut
      cumstain
      cunilingus
      cunnilingus
      cunny
      cunt
      cunt
      c-u-n-t
      cuntface
      cunthunter
      cuntlick
      cuntlicker
      cunts
      d0ng
      d0uch3
      d0uche
      d1ck
      d1ld0
      d1ldo
      dago
      dagos
      dammit
      damn
      damned
      damnit
      dawgie-style
      dick
      dickbag
      dickdipper
      dickface
      dickflipper
      dickhead
      dickheads
      dickish
      dick-ish
      dickripper
      dicksipper
      dickweed
      dickwhipper
      dickzipper
      diddle
      dike
      dildo
      dildos
      diligaf
      dillweed
      dimwit
      dingle
      dipship
      doggie-style
      doggy-style
      dong
      doofus
      doosh
      dopey
      douch3
      douche
      douchebag
      douchebags
      douchey
      drunk
      dumass
      dumbass
      dumbasses
      dyke
      dykes
      ejaculate
      enlargement
      erect
      erection
      erotic
      essohbee
      extacy
      extasy
      f.u.c.k
      fack
      fag
      fagg
      fagged
      faggit
      faggot
      fagot
      fags
      faig
      faigt
      fannybandit
      fart
      fartknocker
      fat
      felch
      felcher
      felching
      fellate
      fellatio
      feltch
      feltcher
      fisted
      fisting
      fisty
      floozy
      foad
      fondle
      foobar
      foreskin
      freex
      frigg
      frigga
      fubar
      fuck
      f-u-c-k
      fuckass
      fucked
      fucked
      fucker
      fuckface
      fuckin
      fucking
      fucknugget
      fucknut
      fuckoff
      fucks
      fucktard
      fuck-tard
      fuckup
      fuckwad
      fuckwit
      fudgepacker
      fuk
      fvck
      fxck
      gae
      gai
      ganja
      gay
      gays
      gey
      gfy
      ghay
      ghey
      gigolo
      glans
      goatse
      godamn
      godamnit
      goddam
      goddammit
      goddamn
      goldenshower
      gonad
      gonads
      gook
      gooks
      gringo
      gspot
      g-spot
      gtfo
      guido
      h0m0
      h0mo
      handjob
      he11
      hebe
      heeb
      hell
      hemp
      heroin
      herp
      herpes
      herpy
      hitler
      hiv
      hobag
      hom0
      homey
      homo
      homoey
      honky
      hooch
      hookah
      hooker
      hoor
      hootch
      hooter
      hooters
      horny
      hump
      humped
      humping
      hussy
      hymen
      inbred
      incest
      injun
      j3rk0ff
      jackass
      jackhole
      jackoff
      jap
      japs
      jerk
      jerk0ff
      jerked
      jerkoff
      jism
      jiz
      jizm
      jizz
      jizzed
      junkie
      junky
      kike
      kikes
      kinky
      kkk
      klan
      knobend
      kooch
      kooches
      kootch
      kraut
      kyke
      labia
      lech
      leper
      lesbians
      lesbo
      lesbos
      lez
      lezbian
      lezbians
      lezbo
      lezbos
      lezzie
      lezzies
      lezzy
      lmao
      lmfao
      loin
      loins
      lube
      lusty
      mams
      massa
      masterbate
      masterbating
      masterbation
      masturbate
      masturbating
      masturbation
      maxi
      menses
      menstruate
      menstruation
      meth
      m-fucking
      mofo
      molest
      moolie
      moron
      motherfucka
      motherfucker
      motherfucking
      mtherfucker
      mthrfucker
      mthrfucking
      muff
      muffdiver
      murder
      muthafuckaz
      muthafucker
      mutherfucker
      mutherfucking
      muthrfucking
      nad
      nads
      naked
      napalm
      nappy
      nazi
      nazism
      negro
      nigga
      niggah
      niggas
      niggaz
      nigger
      nigger
      niggers
      niggle
      niglet
      nimrod
      ninny
      nipple
      nooky
      nympho
      opiate
      opium
      oral
      orally
      organ
      orgasm
      orgasmic
      orgies
      orgy
      ovary
      ovum
      ovums
      p.u.s.s.y.
      paddy
      paki
      pantie
      panties
      panty
      pastie
      pasty
      pcp
      pecker
      pedo
      pedophile
      pedophilia
      pedophiliac
      pee
      peepee
      penetrate
      penetration
      penial
      penile
      penis
      perversion
      peyote
      phalli
      phallic
      phuck
      pillowbiter
      pimp
      pinko
      piss
      pissed
      pissoff
      piss-off
      pms
      polack
      pollock
      poon
      poontang
      porn
      porno
      pornography
      pot
      potty
      prick
      prig
      prostitute
      prude
      pube
      pubic
      pubis
      punkass
      punky
      puss
      pussies
      pussy
      pussypounder
      puto
      queaf
      queef
      queef
      queer
      queero
      queers
      quicky
      quim
      racy
      rape
      raped
      raper
      rapist
      raunch
      rectal
      rectum
      rectus
      reefer
      reetard
      reich
      retard
      retarded
      revue
      rimjob
      ritard
      rtard
      r-tard
      rum
      rump
      rumprammer
      ruski
      s.h.i.t.
      s.o.b.
      s0b
      sadism
      sadist
      scag
      scantily
      schizo
      schlong
      screw
      screwed
      scrog
      scrot
      scrote
      scrotum
      scrud
      scum
      seaman
      seamen
      seduce
      semen
      sex
      sexual
      sh1t
      s-h-1-t
      shamedame
      shit
      s-h-i-t
      shite
      shiteater
      shitface
      shithead
      shithole
      shithouse
      shits
      shitt
      shitted
      shitter
      shitty
      shiz
      sissy
      skag
      skank
      sleaze
      sleazy
      slut
      slutdumper
      slutkiss
      sluts
      smegma
      smut
      smutty
      snatch
      sniper
      snuff
      s-o-b
      sodom
      souse
      soused
      sperm
      spic
      spick
      spik
      spiks
      spooge
      spunk
      steamy
      stfu
      stiffy
      stoned
      stroke
      stupid
      suck
      sucked
      sucking
      sumofabiatch
      t1t
      tampon
      tard
      tawdry
      teabagging
      teat
      terd
      teste
      testee
      testes
      testicle
      testis
      thrust
      thug
      tinkle
      tit
      titfuck
      titi
      tits
      tittiefucker
      titties
      titty
      tittyfuck
      tittyfucker
      toke
      toots
      tramp
      transsexual
      trashy
      tubgirl
      turd
      tush
      twat
      twats
      ugly
      undies
      unwed
      urinal
      urine
      uterus
      uzi
      vag
      vagina
      valium
      viagra
      virgin
      vixen
      vodka
      vomit
      voyeur
      vulgar
      vulva
      wad
      wang
      wank
      wanker
      wazoo
      wedgie
      weed
      weenie
      weewee
      weiner
      weirdo
      wench
      wetback
      wh0re
      wh0reface
      whitey
      whiz
      whoralicious
      whore
      whorealicious
      whored
      whoreface
      whorehopper
      whorehouse
      whores
      whoring
      wigger
      womb
      woody
      wop
      wtf
      x-rated
      xxx
      yeasty
      yobbo
      zoophile
    }
    #words = %w{wtf omg roflcopter rofl lol zomg}
    #words = %w{hack}
    #words = %w{todo}
    #words = %w{workaround}
    profanity = {}
    commit_message_count = 0
    profanity_count = 0
    messages_with_profanity = []
    word_frequency = {}
    Dir.glob("language-commits*.yml").each do |file|
      language = file.match(/\[(.+)\]/).captures[0]
      profanity[language] ||= 0
      YAML.load_file(file).each do |message|
        message[:message].split(" ").each do |word|
          word.downcase!
          if words.include?(word)
            profanity[language] += 1
            profanity_count += 1
            word_frequency[word] ||= 0
            word_frequency[word] += 1
            messages_with_profanity << message[:message]
          elsif word == ":message:"
            commit_message_count +=1
          end
        end
      end
    end
    File.open('profanity_word_frequency.yml', 'w') do |file|
      file.write(YAML.dump(word_frequency))
    end
    File.open('profanity.yml', 'w') do |file|
      file.write(YAML.dump(messages_with_profanity))
    end
    puts "Keys   " +  profanity.map{|k,v| v}.join(" ")
    puts "Values " +profanity.map{|k,v| k}.join(" ")
    puts profanity
    puts "#{commit_message_count}/#{profanity_count}"
  end

  desc "Show all messages ordered by their frequency"
  task :message_frequency do
    system %{grep -h message commit*.yml | sort | uniq -c | sort -r | sed s/"  :message: "//}
  end

  desc "Show all words ordered by their frequency"
  task :word_frequency do
    system <<-COMMAND
      grep message: commit*.yml | sed s/"  :message: "// | awk '
      {
        for (i=1;i<=NF;i++)
        count[$i]++
      }
      END {
        for (i in count)
        print count[i], i
      }' $* | sort -rn
    COMMAND
  end

end


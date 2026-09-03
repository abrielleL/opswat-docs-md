<!-- source: https://www.opswat.com/docs/cm/secure-access-solution/pingone-federate-idp-mfa-setup-guide -->

# Ping Federate IdP MFA Setup Guide

Ping Federate Info:

Ping version: 12.20:

![](https://uploads.developerhub.io/prod/97qW/2fdf0nciccteu6kk1t9r340a2h1i8n8ckiot6ce6mg7dsk8tiy7uhhb5uxhzo1fb.png)

Ping Federate Console Page:

[https://ma-portal-stg.opswat.com:9999/](https://ma-portal-stg.opswat.com:9999/) Credential: ping @Trung Dang Duc  for the access

Ping Federate Pre-configuration

![](https://uploads.developerhub.io/prod/97qW/fqbk9a6i8uafzw3ni1zhl1928cnr2y1ngho56vz0l43k2tmnsla238xp1anzs4xo.png)

If advanced customization option is not displayed, please follow this doc from Ping to enable the option:

[Configuring request parameters and SSO URLs | PingFederate Server](https://docs.pingidentity.com/pingfederate/latest/administrators_reference_guide/pf_config_request_parameter_sso_url.html)

Below is document from Ping to setup Ping Federation to include ACS url inside saml request in IDP Connection:

[Specifying SSO service URLs (SAML) | PingFederate Server](https://docs.pingidentity.com/pingfederate/latest/administrators_reference_guide/pf_specifying_sso_service_urls_saml.html)

Setup Signing Certificate

![](https://uploads.developerhub.io/prod/97qW/wjzxj3vw7ikx4vha2z6e81wwdc0gv9wbv3j4oi6yjhykpo4eao0f9s5fgq1gi4kk.png)

![](https://uploads.developerhub.io/prod/97qW/6htk07nabqr0w1e8vibi0qxxa8nogxjsm6ln9en71u41grhq91x809bmo4vv4nxd.png)

![](https://uploads.developerhub.io/prod/97qW/4z7jbccrxece85h7iwecuk80kym3y1beoxv1l8wedp2hkp1jbfx8zrj3togiddzw.png)

![](https://uploads.developerhub.io/prod/97qW/fpkj9g6sxszeo6mln4mwv2tqvd5wffzhmc1gbu79uyit57bj80drpk4ugu1yyvca.png)

![](https://uploads.developerhub.io/prod/97qW/ft8kd4sxc9dhziapphlml0mbedyzrsqsno7mechyumv8z6x87po46pp719farl7e.png)

Setup simple password validator

![](https://uploads.developerhub.io/prod/97qW/lpkts030gw0awb189w6sd8u720yozka0mzsn3wofyff47wskju7h3fnzbiprh0cf.png)

![](https://uploads.developerhub.io/prod/97qW/no1b2noxof3ha5dl3ej0oyd3krmr31oaj70fmm2xw960yek06wib13scwxv2z6c1.png)

![](https://uploads.developerhub.io/prod/97qW/9bxq3afj4zwjq07ht7aqxyt0s193hopx5hcu8408bsamt1a9q8lnpm78xve8p53n.png)

![](https://uploads.developerhub.io/prod/97qW/kiad503cmvkw57vaxomm8ohq89omyqf25v0ghvqfy5s21tj53pbxbxs2ba0my6tf.png)

![](https://uploads.developerhub.io/prod/97qW/crmjmqkpuy9v6fs5uyw8hu6492wmvb7pj21rfsospomunh4abwoji5qc7po9us9x.png)

![](https://uploads.developerhub.io/prod/97qW/1t4izw1w8opiwh6t8l1ecgegu83v6tvmi46ojg0kf5ehma9vac3vszusehiy24qm.png)

![](https://uploads.developerhub.io/prod/97qW/m04htglc5mce2fd7iu7s8a1387lla3noylpom7qvkzeg4cd0pzr65ztd09uausqd.png)

Create SP Connection

Select Application → SP Connections

![](https://uploads.developerhub.io/prod/97qW/zxrd69go7rnjldsj03e9tpws2ekcwy3z92nktnrkhkn4rkfkpuootcfe02dexsya.png)

![](https://uploads.developerhub.io/prod/97qW/50pepajgsvkbrsg2cs2kesvrcl5ijqnfv7i2w7rs96jinnghjnsm72ybhcql7z8a.png)

![](https://uploads.developerhub.io/prod/97qW/2dcadqck1d7xhosd1i4ci1mp20gdkawm34adih2h7uxnxarsv3nksxd2efq7a715.png)

![](https://uploads.developerhub.io/prod/97qW/gwf1e7akfwgfrree5z6zi0y58qe54ornh9ddbfupdei7dq1un4svndhg42y8fp9a.png)

![](https://uploads.developerhub.io/prod/97qW/qdk46xgyq1xgwlvj7lbnfx2va0pxozsjvcyjrso6pqha2lld9ngh9jtpbn2r2kdu.png)

![](https://uploads.developerhub.io/prod/97qW/licfm8et3txdexjrcgzp5012ovajkjk2mrm082b4llqo1yr3a797vl77wlqi37q6.png)

![](https://uploads.developerhub.io/prod/97qW/ug4cedbohb7b2l7hafwp0omxzaxqxqbzo3w7rnwi13yywbusa6gj6tvptwnevnpa.png)

![](https://uploads.developerhub.io/prod/97qW/m435d92xfoboxbqhqukgv8olavjzdd6ufsbzmss6fwpsucdsslsifozi4hxpvx1p.png)

![](https://uploads.developerhub.io/prod/97qW/23foa234g92s69p8o16hz3xymc3h8bgv9hzc025uwnfenj2hli0vkv0neteq2fz8.png)

![](https://uploads.developerhub.io/prod/97qW/ng9ah8rre8lygh0zuky6qunbdr9q83kz8m2kzvza3hs2bifi6iv6q1egz2ohcjye.png)

![](https://uploads.developerhub.io/prod/97qW/o72zsal051hk2nh194gp5uce3h0wcozd1tz5isounl3mra0kj0pv1hblxkgzy1xg.png)

![](https://uploads.developerhub.io/prod/97qW/rljrhrgn6r7o2sagkt98k0qaxizkcbmoy9crbyiw1nn7pff7fibjib0ftmhfhifw.png)

![](https://uploads.developerhub.io/prod/97qW/4jgdofnmkbeqykxh9j45trsgovhjd438ttsqp4ejmtfmoqik7dzqtayw8ac401km.png)

![](https://uploads.developerhub.io/prod/97qW/zhl3i48iqktz8dm2x5c09vtzas9au0xwiqpmx4qzgac90w86liiri4c7wjnq121y.png)

![](https://uploads.developerhub.io/prod/97qW/8rajkqip63ttkpwffxaf71rkujm8qoh465copzt7y4u88y9ccfb2dckn9ztnc67i.png)

![](https://uploads.developerhub.io/prod/97qW/l0pnxs1sq4pcvy1w6kcklpwqx29x8abbcatx0p2le38p79gl6oxm29lp2l3e68q2.png)

![](https://uploads.developerhub.io/prod/97qW/uo8sgf8y79kn48o62pls820eqlw71oisebtr7bl8v01tbywctepc6y9sfgnko2c8.png)

![](https://uploads.developerhub.io/prod/97qW/kajp4ad5q5kmj6bt5rdc8zja6gzswicar1q7gd2scrasxavquu57xrs8m8l9m4nm.png)

![](https://uploads.developerhub.io/prod/97qW/1wdpao8reiikpxdhk3mu953yke3frjmqbb6pt7qk3rdvntzi62i3sj4l0u9o73j5.png)

![](https://uploads.developerhub.io/prod/97qW/1z5j78oplcpivxx5vbxbeqz4yow5tyerw6ze72aw8e0j2hefnuorsc9d6zpsycft.png)

![](https://uploads.developerhub.io/prod/97qW/wzumtd8s0cm2eifwifddi9qrzabta6o1x290uhyziyaow978g1mk7fh20eih5x3s.png)

![](https://uploads.developerhub.io/prod/97qW/a1cww4br3rddyx4pjmt6zcm92at7huwy0i0xhkg2i81cclc4lzz0lfieaall3p2u.png)

![](https://uploads.developerhub.io/prod/97qW/fthhkmntif0i0c8cl1klt6w1nyq1kswt0f5yquroim86rgx3o8q7h4ji9sdya8ag.png)

![](https://uploads.developerhub.io/prod/97qW/v6qsjex4ccexqng99ap64b0f5qkwhpundkyctj1sbslj9nosyahfkh5mhru44a3e.png)

![](https://uploads.developerhub.io/prod/97qW/svu9sz6miijfjzh87ye4l4fzl1cnieip238agcixx20rrkhs03mqv0hant6qfppy.png)

![](https://uploads.developerhub.io/prod/97qW/czznpxve5q4881ml6zuu6g8ogwceqfts780whpwgjwywl9jeafq3xe4rhpwn02g2.png)

![](https://uploads.developerhub.io/prod/97qW/8n609kbapn0n1liruprwp7klev1cto9xqij973j4wnuaz477ajl5km4shzjvamrf.png)

![](https://uploads.developerhub.io/prod/97qW/4tsqtq09roiefludlzud74wiiaparsntpm4caxpaoowqo6vcc2fmlylxbqmak81m.png)

![](https://uploads.developerhub.io/prod/97qW/ayqisaunlwzok1iy813lvrwujb896ddrzfmzv7sp2n4qiy87ilz1yvbkhboyi1pr.png)

![](https://uploads.developerhub.io/prod/97qW/mehuclt501w7j35w1lq1cg2qkdej47rfc3meo4o9zo9x1bsl4feqt7vfdon1ds78.png)

![](https://uploads.developerhub.io/prod/97qW/2hde4mbji3xc9glep6py4upqodulacq9cnt2xdu66c5qec2j1dwd06vzooq0fda1.png)

![](https://uploads.developerhub.io/prod/97qW/h8m5xrbkzkygop1e7bjht83vvsdmsqmu6z8cecm4yudcdl07q00bex78i3hac2wg.png)

![](https://uploads.developerhub.io/prod/97qW/xerighjamim9zk30npltcgvujo26ptykeuygeol7xh9u9liwtrc5hyafrwhjj10w.png)

![](https://uploads.developerhub.io/prod/97qW/sgc5hb25ln7ym85gyixtbq0m2lzvc8rpfmp17j0vvdm2lbpn51tfuty9yz98mj3a.png)

![](https://uploads.developerhub.io/prod/97qW/cvu8ziw5kvgbf3sbdqsn0kjg6fhgusfo6xw18ovcoq0yggbvw6n7uho143gpap7v.png)

![](https://uploads.developerhub.io/prod/97qW/s2v120c7xty7f2d58pqpdlfqrgckma2l7gxrqim19lxwt9ftzqjlrp3fdtzs8aof.png)

![](https://uploads.developerhub.io/prod/97qW/4n4xhicnfvtppynugbm74m41eilnngum0iupwmskwjmyfmckpjq7djispokwpomb.png)

![](https://uploads.developerhub.io/prod/97qW/m0xvf1j73opgnthslffofii6e5hpd71zxar1qgy8ln17loxwvlxowkk0vq98t0vd.png)

![](https://uploads.developerhub.io/prod/97qW/974uw35i1hukiaezzqr41k9angir3lmqi1atacki6tftvsb1sizr1mxnxk8yj1x1.png)

![](https://uploads.developerhub.io/prod/97qW/en2l39lq7k3qgjdyyjxqxebiay9n0m34vk86qsniy4zukzjil7omxwxjci56ajz9.png)

![](https://uploads.developerhub.io/prod/97qW/izrqduxn3g9br74bzrgnkamq81n7qg1jiwp6zeubtj1hlt3v8yyo1bb3mthonppy.png)

![](https://uploads.developerhub.io/prod/97qW/tbugmvwsp02c14ye2hfrf3rvfydx24hdncd5ylgru2owqnhd4ochgfhnb7jawijf.png)

![](https://uploads.developerhub.io/prod/97qW/te4653howody3z4dvukqa7rihc0y5b7hcvja3rwp618a2mn8knwykijplugx214x.png)

![](https://uploads.developerhub.io/prod/97qW/dk6lbhhunz6dfw5ivb1lq6v2hztgofsodb46151sf4pgylnyuewdwf1062rvitig.png)

![](https://uploads.developerhub.io/prod/97qW/wckp1pljp71bmq8jozz38qpte2f8m9fxoi6rjl941m62c3wrlc9f5hg9p13r7f1v.png)

Create IdP Adapter for Ping Internal authentication (simple password html authentication)

![](https://uploads.developerhub.io/prod/97qW/3clippmmu8tv97uxmfs9oytounegmuehhq22pfx895u0fhu2aw74z08ge4fy3kvh.png)

![](https://uploads.developerhub.io/prod/97qW/ld2zpqdj478mw5nzx2ohxapni6c1cc4czbadm6t665db84btdmgpbsgzvskz4uda.png)

![](https://uploads.developerhub.io/prod/97qW/nsky0wlrklovj17yyi25muyzsw0vj7owvrsmvsjfjqqbx6up06jzx53y9c8jdcuq.png)

![](https://uploads.developerhub.io/prod/97qW/gixlop8l3bck8acympiu7s0vgrvgxur5rjb4qvi2nsoy57lyycgafiskr9liuvqo.png)

![](https://uploads.developerhub.io/prod/97qW/yn6wznk5cpejnh9dsrg904hf8ng4tma1f9wzkud6mq4rv2haz0svilm4j9m954bg.png)

![](https://uploads.developerhub.io/prod/97qW/pzqxqstxdvnpeb8oe1y8gk5a2t4hgeowku2w2t2d2nmjtfuaz9zhlzbw4xioncvl.png)

![](https://uploads.developerhub.io/prod/97qW/0tgo47ornweta6zfqkksa8qqucv72uhcmfm23st3vdrht9z726u32y5mo8dxevrh.png)

![](https://uploads.developerhub.io/prod/97qW/v161daialviu3975i2qbam51zyi4nq3hjvwt285il32gaoyscorkdxnyoqdergiu.png)

![](https://uploads.developerhub.io/prod/97qW/fa99zmpl6i2c90cn0byttjy5j3rcg94arhju4qortpyibbusziefgm1zphrnhg6l.png)

![](https://uploads.developerhub.io/prod/97qW/j21g6s1i0k34y373o1cwj3yzwk927go3gf1p5lix52wo3foige6bxqst4uc20de1.png)

![](https://uploads.developerhub.io/prod/97qW/sahis4f2shagox51n3dpt7exxe3frgs2d0e07ok53n9g9rot9vizkryqfuiq3fkr.png)

![](https://uploads.developerhub.io/prod/97qW/mevk63w57tnu2gbtuubfjnmdim8d2dpe512kwwpy63uoc32ixxzvbj2rbc9cemic.png)

![](https://uploads.developerhub.io/prod/97qW/1xqjmuy2cd8encthjc66ga701beghyps20k4k0xsqelktbb52lu805xp8xxs2yxb.png)

![](https://uploads.developerhub.io/prod/97qW/759lzqpu0inq58nirpiay5n4r9w0e59s0gzj7pzfs4ekyw30hly3peq9vs1icuqx.png)

![](https://uploads.developerhub.io/prod/97qW/qe8xgibpn9x9is0umh0eu0rn8aoe22ytbdb3lw647f40cucdxt9cfz7is77ssubc.png)

Create IdP connection to connect to OPSWAT IdP MFA service

![](https://uploads.developerhub.io/prod/97qW/yelvd9reuz56e3p899qmz5lqgwfxbmfun52i1bbn1gt7a9w9j3ifpuf010r37m4j.png)

![](https://uploads.developerhub.io/prod/97qW/e2wb33o8t1qcinohsg0m3opnuecw93sosdide4fndduyp6plizy1068t9fhs8fsz.png)

![](https://uploads.developerhub.io/prod/97qW/32jwudzagzu9f4b7jkx79xmxx0oekd87jqccd35h4fqbgoissq1u4ajnj5pf7gd8.png)

![](https://uploads.developerhub.io/prod/97qW/3fmjxggsv6qyon94uzu6bnnmkqbgws410hnt0wwmvbigdsvmao9emfjofmcnvs5j.png)

![](https://uploads.developerhub.io/prod/97qW/myio2qku3ljx7q9aidk8xnjcsuh80fmnsuvruiz9sm5phzgdgwpc80kic78yxzm0.png)

Go to Secure access console on My OPSWAT Central Management to copy Entity Id

![](https://uploads.developerhub.io/prod/97qW/9zbwakikxabhssxukocqmn9yunbehhrr0j775ap32z1l3rslzm8slq8obeqxe9k7.png)

And paste in PARTNER’s ENTITY ID

![](https://uploads.developerhub.io/prod/97qW/bxh2wbbjqg8rcs2vzqxcjun7zocex8igj1bs8lyxfydtgwn7n3r9vftffhvv5muu.png)

![](https://uploads.developerhub.io/prod/97qW/yxkmmnp7gvfk58sumihwuoevrocpg4i1fjar6ggn3pfihtemtzoq7a48hak9f4gj.png)

![](https://uploads.developerhub.io/prod/97qW/96dnpell5istkf9rw7yt3v07surlgcwc0jpp6go2ffiurq8xj5233v7f3xtrmfmo.png)

![](https://uploads.developerhub.io/prod/97qW/mvbmltb5gu436ojppn9p6i0eux257w7bx9eibf2r59ot33h302d5fxjqd2sm0yuh.png)

![](https://uploads.developerhub.io/prod/97qW/bdt6sl4ty0konz7x6miyv72y57iep2nkxosqjfypvvspz551cur5r8zagwpuzrn9.png)

![](https://uploads.developerhub.io/prod/97qW/22jkr1k91jzd0y887zzcqjxthfeb1jl1s55srq3hbwejdo1q4yg6c4sqbdtwdy5d.png)

![](https://uploads.developerhub.io/prod/97qW/suxcio1n8u3z6sdmw7irq3jfyj3x6kw8ktzltfldcwqbwidmxlmxv242gajthvll.png)

![](https://uploads.developerhub.io/prod/97qW/h78soi8cra0dy4vvr09z584mbvlfgfbjsf6fh8o2fogumxneduk6cxjfuo3nxm9z.png)

![](https://uploads.developerhub.io/prod/97qW/b9tml3xdzejsq1lkvb9zu96m5ik7fhsvrwf8a0fgm1i72pi1k0dk92tgb2h32hef.png)

![](https://uploads.developerhub.io/prod/97qW/zptwfjrfprz9sy32dgo96ullwn6uot7qffltku8r8kv7vmx147ffv78demshv0rm.png)

OGNL Expression:

`1. #authnRequest = #AuthnRequestDocument.getAuthnRequest(), `

`2. #authnRequest.setAssertionConsumerServiceURL("https://ma-portal-stg.opswat.com:9031/sp/ACS.saml2")`

The endpoint URL is copied from Secure access page

![](https://uploads.developerhub.io/prod/97qW/hgg60n5ms6y6ldbiq3qujmjrxv64z7f90boc66tzx46itqsjjjp1n7yfdbsd2c2j.png)

![](https://uploads.developerhub.io/prod/97qW/96ju6tzml0311quex79bcgb2e8sbr5tim1gkmrtznapp3i522oulogxm3e9e0ggh.png)

![](https://uploads.developerhub.io/prod/97qW/0jr7nny2yw3cota6f3sa0v01j0d6ux14du8dbe1lu5xa3yo08uhd9myjp5cj6l2u.png)

![](https://uploads.developerhub.io/prod/97qW/3aqeimbri83m290cigjdvj3vmzed4a95iqo7iyoqarygeupqwt87q18mtgqm917q.png)

![](https://uploads.developerhub.io/prod/97qW/65c7nqo22cyjbrcarex7yjahlr06ec69dux0rbi3brmgurum60uh4yhk6fis2o3p.png)

![](https://uploads.developerhub.io/prod/97qW/ab0eb9tgylq92bj5nhtltm7hu8ay8ltkg3af2oji2oqisp3oa39tuw039ww7dcb2.png)

![](https://uploads.developerhub.io/prod/97qW/p92ayjwh74bfh4utp4klqm4ilxenlvi5kq6nwppuxeu7hyaglnurf3c864a7j4e1.png)

![](https://uploads.developerhub.io/prod/97qW/nox0pqt95s7mj3dv35dfgxjzato2g5ipjpy1d6x5nvahuk5seyu9rc7ievhtno0f.png)

![](https://uploads.developerhub.io/prod/97qW/z8nrwjlp4ivjgb9uaowsq1lxm8u0qlu55e4k36ad66e5p7p1kwdndblowdc7dle4.png)

![](https://uploads.developerhub.io/prod/97qW/rh0cimp9xb0psft0i2ezjt0uc8w0oibdkeoa2uxipu89v683jdrbnmini7y3qcbx.png)

![](https://uploads.developerhub.io/prod/97qW/vsdrnadf9a5kdccmid6wx4bu5hlm5gchqs3uby2k3k3r6dngkszoumrk9xfir9gc.png)

![](https://uploads.developerhub.io/prod/97qW/gyqha1tyeys2n1k7e7s5azcx1sk06isjzhtfo72gg2ngzusyjout7lwqwh6e6thz.png)

![](https://uploads.developerhub.io/prod/97qW/9m84tr0ferfzl1ghra5591fz1bex1xpgwks7x4lwpz538vsd9hf0x6lprpicnjkk.png)

![](https://uploads.developerhub.io/prod/97qW/h1j3le0m8pr0qrety5d6rccf096lqs0j6r72r1u3ex3tlsr3qijzk51s6aequzjo.png)

![](https://uploads.developerhub.io/prod/97qW/hq8b9g9o36h8jsielu5zeix2fb1cp8z2ut455ul63nodn60dg52nqc1kz9hnj5rd.png)

![](https://uploads.developerhub.io/prod/97qW/3rmm7zhysxygu4bg8wmmjmds6ca6mlx5uqlmk7br8ydvj5cu9llcd0bl358uj6ei.png)

![](https://uploads.developerhub.io/prod/97qW/9r46dttid9cbzyt77gkgp5dzekq2dt2kdfjhhzs6kb10d03n7eewv1qurz763ars.png)

![](https://uploads.developerhub.io/prod/97qW/6rmaa7mfjfrh1ce8kuqi1z02dh1czmktl1nzn4jxxvazhfhr4y3xrt3u07zyeuvv.png)

![](https://uploads.developerhub.io/prod/97qW/l90y8ei0j9yrilchnsznxfy0si6cy611miahjj4mgubei1s10izve72zhuw6nc35.png)

![](https://uploads.developerhub.io/prod/97qW/zbpg165wt7k6kfot296nxpdj97g8a5pv4wa8k9xbtuahc584tgmp1wsrcb286one.png)

![](https://uploads.developerhub.io/prod/97qW/brlpef8ylmzwbz1zixtn5y2rphhfs4k2xluf9en6gmz2yrzujx1mlfxfu1tvy24i.png)

![](https://uploads.developerhub.io/prod/97qW/sy8w0klopa15yenpvachq0ze2loi0gjgyokgd9mo6ieivufhrqkui31wag2jlx69.png)

![](https://uploads.developerhub.io/prod/97qW/hnigectubgnuoemxrko4nx29l7f8mzw82jzdh8qt9vyszbpvqd1tobjufcoznf2g.png)

![](https://uploads.developerhub.io/prod/97qW/c8ykjpy8xv50hs1ijfqqhofplyl6154ewyorww3cd4ru4jcs2q61pihhuot2gv4r.png)

![](https://uploads.developerhub.io/prod/97qW/os7zjppjxd6ciuuvceewm5sznxi18kp8dc546489mx8gmqzf0c9ltebcd8qp2i1p.png)

![](https://uploads.developerhub.io/prod/97qW/kkg6u4s4qt3l620kn1qh7a9zzppz0vokfcy9d4c5v3kpg6fottf0vc7nd0045yk2.png)

Import IdP connection to IT Access IDP MFA

![](https://uploads.developerhub.io/prod/97qW/v0e96hotqt01hh5rgu3hb7ydnf3jvjdxps0xlp4zlfqo8fwrl3hiw8pw0ch27tei.png)

![](https://uploads.developerhub.io/prod/97qW/ezba3k9212izsauoh7t1skr2khyumnne47urmhfwzg1gx1xa4kwb0g9nui6pazo2.png)

![](https://uploads.developerhub.io/prod/97qW/kp3qsbj8pjgnao1pd9q8jt3dokfm3be28egweh8svx35yr2wmxwywc65ya859z1k.png)

Upload to Secure Access IDP MFA page:

![](https://uploads.developerhub.io/prod/97qW/d63l3fsaw7d070za8etic01es10wa9fve01v1wrixqochsz2t1p4xssye5jh3t9x.png)

Setup Ping Federation Policy ( flow)

![](https://uploads.developerhub.io/prod/97qW/7epgnfw1mi3s7qyqatxj1oolh22rzqdai60z6cjc84uozjnv90pa2ozy5aoapiut.png)

![](https://uploads.developerhub.io/prod/97qW/zkybqebkx0hhmeio1t8zypccu6al8pmb4bft9xyp19fphytidqwzhjov5ox1ci60.png)

![](https://uploads.developerhub.io/prod/97qW/1ma1m5dbomsz9wphff83v9kcqtqx6rxb2gr9or1mu96m13ehl56hr9drwjodv27g.png)

![](https://uploads.developerhub.io/prod/97qW/8qdcujpdnoz6ilqnx4m7qnbtteam9qm6frrjjin5r303x2izb0nhcqv18y7l85ce.png)

![](https://uploads.developerhub.io/prod/97qW/htd99msl1k8d1nnx15u6dudo7olztk4qnqhk4biyss8pnr7s7itx633g0sgl9svi.png)

![](https://uploads.developerhub.io/prod/97qW/3lagg72vvmqhb7x4tuzyzwm64l2v5ivfqorn9q4efzj1gljit9a3umxv6uyz398h.png)

![](https://uploads.developerhub.io/prod/97qW/4wnr50c9qt1rvib3cyujl6bqjam0kh8j2gpzr5293szw4gbg7agf7fj8ccfwkqpy.png)

![](https://uploads.developerhub.io/prod/97qW/n4o0ofs8yqgpwoema8ktjifh0t1mqi04tsgrt2aq99ot3ijfuza1xzbifgs15oce.png)

![](https://uploads.developerhub.io/prod/97qW/ghzvs5jgboo1mln2j59alb79nzjbbf5l2smoo75xn5wohjz94quohotrn8y5ohvm.png)

![](https://uploads.developerhub.io/prod/97qW/5uhudd4q7gywogpfcrnv32u45h6ybg08tgh05vssy2s1pkgwtbkvpgih2b2fnu0x.png)

![](https://uploads.developerhub.io/prod/97qW/qzd812m2njtd2y7a29r9l01l9jzhwhq8nz1uyha8h58ec7how5jc6wpfpcbhwqy8.png)

![](https://uploads.developerhub.io/prod/97qW/0d8qdz9pdix9b5dftfd0xn41fit0h2o73shv1muul9p7fdu5v0dquluyc160qtsb.png)

![](https://uploads.developerhub.io/prod/97qW/28idttmdlbskpt14lcboqtxyd2geppw9308w4ilvu3srrotqdbcjc83wwjsa5ldk.png)

![](https://uploads.developerhub.io/prod/97qW/r5xh58dwuem8nfhg13emm48183w459gfbmdg1xp8z065l3buy828r23237pzy78z.png)

How to test"

Install OPSWAT Endpoint staging

Go to SP connection:

![](https://uploads.developerhub.io/prod/97qW/743b3gld3ecm2qqjlv865xy6y2in2jrw69ufj45j8hd0jkri1dfioh2rjcnrvzfl.png)

Access the link:

[https://ma-portal-stg.opswat.com:9031/idp/startSSO.ping?PartnerSpId=IAMShowcaseTest](https://ma-portal-stg.opswat.com:9031/idp/startSSO.ping?PartnerSpId=IAMShowcaseTest)

![](https://uploads.developerhub.io/prod/97qW/yuiym5yv2g4n3s4uqp3cn69aemx20sftfrpx1zbaug7vjswzmvohpp6sfuxidfgz.png)

Enter username & password setup in Simple Password HTML IDP adapter:

![](https://uploads.developerhub.io/prod/97qW/bz05qbtbiv9ojmrqkp0vkag0ltws5ij9uma4j8pcbgt22nkep4p8zgr2k91yubut.png)

ex: trung - 123456

Non-com:

![](https://uploads.developerhub.io/prod/97qW/i3ubqy9ym69swi8lu3jg5r0v4xr2e34f2ol1w3sjf66wlnc12zartu8cw1e9x4yb.png)

Compliance:

![](https://uploads.developerhub.io/prod/97qW/ixuyowgycebfv9w2d2zqioqa2lhl0hc35vizmfg9i48vkowdqwczreo5by1a7agw.png)

Meeting with Ping:

[PingFed & OPSWAT Configuration-20250206_220311-Meeting Recording.mp4](https://opswat2017-my.sharepoint.com/personal/tle_opswat_com/_layouts/15/stream.aspx?id=%2Fpersonal%2Ftle%5Fopswat%5Fcom%2FDocuments%2FRecordings%2FPingFed%20%26%20OPSWAT%20Configuration%2D20250206%5F220311%2DMeeting%20Recording%2Emp4&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2Ef3387c5f%2Dc150%2D48cb%2D8728%2D8e26e9431270)

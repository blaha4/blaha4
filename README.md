using System;
using System.Collections.Generic;

class Zavodnik : IComparable<Zavodnik>
{
    public int StartovniCislo { get; set; }
    public string Jmeno { get; set; }
    public long Cas { get; set; }

    public override int GetHashCode() => StartovniCislo.GetHashCode();
    public override bool Equals(object obj) => obj is Zavodnik zavodnik && StartovniCislo == zavodnik.StartovniCislo;
    public int CompareTo(Zavodnik other)
    {
        int result = Cas.CompareTo(other.Cas);
        return result != 0 ? result : Jmeno.CompareTo(other.Jmeno);
    }
}

class EvidenceZavodniku
{
    private HashSet<Zavodnik> zavodnici = new HashSet<Zavodnik>();
    private SortedSet<Zavodnik> setrideniZavodnici = new SortedSet<Zavodnik>();

    public void PridatZavodnika(Zavodnik zavodnik)
    {
        if (zavodnici.Add(zavodnik))
        {
            setrideniZavodnici.Add(zavodnik);
        }
    }

    public HashSet<Zavodnik> Zavodnici => zavodnici;
    public SortedSet<Zavodnik> SetrideniZavodnici => setrideniZavodnici;
}

using System;
using System.Collections.Generic;

enum TypKarty { Permanent, Creature, Enchantment, Artifact, Planeswalker, Sorcery, Instant, Plane, Tribal, Conspiracy }

class Karta
{
    public string Nazev { get; set; }
    public TypKarty Typ { get; set; }
}

class EvidenceKaret
{
    private string jmenoHrace;
    private List<Karta> kartyHrace = new List<Karta>();

    public EvidenceKaret(string jmenoHrace)
    {
        this.jmenoHrace = jmenoHrace;
    }

    public void PridatKartu(Karta karta)
    {
        kartyHrace.Add(karta);
    }

    public List<Karta> SeznamTypu(TypKarty typ)
    {
        return kartyHrace.FindAll(karta => karta.Typ == typ);
    }
}






using System;
using System.Collections.Generic;

class Zak : IComparable<Zak>
{
    public string Jmeno { get; set; }
    public string Prijmeni { get; set; }
    public int CisloVeVykazu { get; set; }

    public override int GetHashCode() => CisloVeVykazu.GetHashCode();
    public override bool Equals(object obj) => obj is Zak zak && CisloVeVykazu == zak.CisloVeVykazu;
    public int CompareTo(Zak other) => Prijmeni.CompareTo(other.Prijmeni);
}

class EvidenceZaku
{
    private HashSet<Zak> zaci = new HashSet<Zak>();
    private SortedSet<Zak> setrideniZaci = new SortedSet<Zak>();

    public void PridatZaka(Zak zak)
    {
        if (zaci.Add(zak))
        {
            setrideniZaci.Add(zak);
        }
    }

    public HashSet<Zak> Zaci => zaci;
    public SortedSet<Zak> SetrideniZaci => setrideniZaci;
}

using System;
using System.Collections.Generic;

enum TridaMineralu { Prvky, Sulfidy, Halogenidy, OxidyHydroxidy, Uhlicitany, Sirany, Fosforecnany, Kremicitany, OrganickeMineraly }

class Mineral
{
    public string Nazev { get; set; }
    public TridaMineralu Trida { get; set; }
}

class SberatelMineralu
{
    private string jmenoSberatele;
    private List<Mineral> mineralySberatele = new List<Mineral>();

    public SberatelMineralu(string jmenoSberatele)
    {
        this.jmenoSberatele = jmenoSberatele;
    }

    public void PridatMineral(Mineral mineral)
    {
        mineralySberatele.Add(mineral);
    }

    public List<Mineral> SeznamTridy(TridaMineralu trida)
    {
        return mineralySberatele.FindAll(mineral => mineral.Trida == trida);
    }
}

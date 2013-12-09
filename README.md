// Magic damage, check for resists

     if ((schoolMask & SPELL_SCHOOL_MASK_NORMAL) == 0)
     {

-        float victimResistance = float(victim->GetResistance(GetFirstSchoolInMask(schoolMask)));

+        float victimResistance = float(victim->GetResistance(schoolMask));

         victimResistance += float(GetTotalAuraModifierByMiscMask(SPELL_AURA_MOD_TARGET_RESISTANCE, schoolMask));
         
     {

+        AuraEffect=032 ( AuraResist 010 ) = GetAuraModifier (SPELL_AURA_EFFECT_RESIST)
         

         if (Player* player = ToPlayer())
         
         

@@ -17386,7 +17386,7 @@ uint32 Unit::GetRemainingPeriodicAmount(uint64 caster, uint32 spellId, AuraType

     AuraEffectList const& periodicAuras = GetAuraEffectsByType(auraType);

     for (AuraEffectList::const_iterator i = periodicAuras.begin(); i != periodicAuras.end(); ++i)

     {

-        if ((*i)->GetCasterGUID() != caster || (*i)->GetId() != spellId || (*i)->GetEffIndex() != effectIndex || (*i)->GetTotalTicks() == 0)

+        if ((*i)->GetCasterGUID() != caster || (*i)->GetId() != spellId || (*i)->GetEffIndex() != effectIndex || !(*i)->GetTotalTicks())

             continue;

         amount += uint32(((*i)->GetAmount() * std::max<int32>((*i)->GetTotalTicks() - int32((*i)->GetTickNumber()), 0)) / (*i)->GetTotalTicks());

         break;

@@ -17402,6 +17402,17 @@ void Unit::SendClearTarget()
             
             

     SendMessageToSet(&data, false);

 }

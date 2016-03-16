---
layout: post
title: Java remove accent from string
---

I was recently importing data from various sources, some of which had
some non-standard (unicode) characters. In particular I wanted a way to
remove the accents from french letters from **á** to **a**  








I stumbled across this code which does the job perfectly:








    /**
         * replace accented characters with their unicode equivalent
         * @param str
         * @return
         */
        public static String deAccent(String str) {
            String nfdNormalizedString = Normalizer.normalize(str, Normalizer.Form.NFD); 
            Pattern pattern = Pattern.compile("p{InCombiningDiacriticalMarks}+");
            return pattern.matcher(nfdNormalizedString).replaceAll(""); 



 } 



 










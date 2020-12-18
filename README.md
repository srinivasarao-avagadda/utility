public static JSONObject safeGetJSONObjectFromMultipleKeySingleValue(JSONArray jArr,
                                                                         String key,
                                                                         String value) throws Exception
    {
        JSONObject jObj = null;
        try
        {
            if (jArr != null & key != null & value != null)
            {
                for (int i = 0; i < jArr.length(); i++)
                {
                    JSONObject jObjTemp = (JSONObject) jArr.getJSONObject(i);

                    String valueTemp = null;
                    valueTemp = (String) JSONUtils.safeGetJSONObject(key, jObjTemp);

                    if (jObjTemp != null && !jObjTemp.isNull(key) && valueTemp.equals(value))
                    {
                        jObj = jObjTemp;
                        break;
                    }
                }
            }
        }
        catch (Exception e)
        {
            throw e;
        }
        return jObj;
    }

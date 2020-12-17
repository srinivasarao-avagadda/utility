public static int getIntValue(String value, int defaultValue) {
    int toRet = defaultValue;
    if (!StringUtils.isEmpty(value)) {
      toRet = Integer.valueOf(value);
    }
    return toRet;
  }

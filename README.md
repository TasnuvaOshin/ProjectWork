# ProjectWork

   /*
 Hide the Key Board Main KeyBoard HIDE SYSTEM 
  */
    public void hideKeyboard(Activity activity) {

        ////Show
        //        imm.toggleSoftInput(InputMethodManager.SHOW_IMPLICIT, 0);


        // ContentView is the root view of the layout of this activity/fragment
        root.getViewTreeObserver().addOnGlobalLayoutListener(
                new ViewTreeObserver.OnGlobalLayoutListener() {
                    @Override
                    public void onGlobalLayout() {

                        Rect r = new Rect();
                        root.getWindowVisibleDisplayFrame(r);
                        int screenHeight = root.getRootView().getHeight();

                        // r.bottom is the position above soft keypad or device button.
                        // if keypad is shown, the r.bottom is smaller than that before.
                        int keypadHeight = screenHeight - r.bottom;

                        Log.d(TAG, "keypadHeight = " + keypadHeight);

                        if (keypadHeight > screenHeight * 0.15) { // 0.15 ratio is perhaps enough to determine keypad height.
                            // keyboard is opened
                            if (!isKeyboardShowing) {
                                isKeyboardShowing = true;
                                onKeyboardVisibilityChanged(true);
                                InputMethodManager imm = (InputMethodManager) getActivity().getSystemService(Activity.INPUT_METHOD_SERVICE);
                                //Hide:
                                imm.toggleSoftInput(InputMethodManager.HIDE_IMPLICIT_ONLY, 0);
                            }
                        } else {
                            // keyboard is closed
                            if (isKeyboardShowing) {
                                isKeyboardShowing = false;
                                onKeyboardVisibilityChanged(false);
                            }
                        }
                    }
                });
    }

    void onKeyboardVisibilityChanged(boolean opened) {
        Log.d("keyboard ", String.valueOf(opened));
    }

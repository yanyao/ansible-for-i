..
.. SPDX-License-Identifier: Apache-2.0
..

:github_url: https://github.com/LiJunBJZhu/i_collection_core/tree/master/plugins/modules/ibmi_save_product_to_savf.py


ibmi_save_product_to_savf -- Save the the licensed program(product) to a save file
==================================================================================

.. contents::
   :local:
   :depth: 1


Synopsis
--------

the ``ibmi_save_product_to_savf`` module save the product to a save file on the target ibmi node.






Parameters
----------

  check_signature (optional, str, *SIGNED)
    Specifies if the digital signatures of objects being saved with the licensed program are to be checked


  product (True, str, None)
    Specifies the seven-character identifier of the licensed program that is saved


  option (optional, str, *BASE)
    Specifies the optional parts of the licensed program given in the Product prompt (LICPGM parameter) that are saved


  language (optional, str, *PRIMARY)
    Specifies which national language version (NLV) is used for the save operation

    It's the IBM-supplied language feature codes, like German is 2924, English is 2924

    This parameter is ignored when object_type(*PGM) is specified


  object_type (optional, str, *ALL)
    Specifies the type of licensed program objects being saved


  target_release (optional, str, *CURRENT)
    Specifies the release level of the operating system on which you intend to restore and use the product


  release (optional, str, *ONLY)
    Specifies which version, release, and modification level of the licensed program is saved


  savf_name (True, str, None)
    Specify the name of the save file, if it is not existed, will create it


  joblog (optional, bool, False)
    If set to ``true``, output the avaiable JOBLOG even the rc is 0(success).


  savf_library (True, str, None)
    Specify the name of the library where the save file is located, if it is not existed, will create it


  parameters (optional, str,  )
    The parameters that SAVLICPGM command will take. Other than options above, all other parameters need to be specified here.

    The default values of parameters for SAVLICPGM will be taken if not specified.

    Parameter CLEAR in SAVLICPGM command should not be specified here, 'CLEAR(*ALL)' already used.







See Also
--------

.. seealso::

   :ref:`ibmi_uninstall_product, ibmi_install_product_from_savf_module`
      The official documentation on the **ibmi_uninstall_product, ibmi_install_product_from_savf** module.


Examples
--------

.. code-block:: yaml+jinja

    
    - name: Saving Program using Defaults
      ibmi_save_product_to_savf:
        product: 5770WDS
        savf_name: MYFILE
        savf_library: MYLIB

    - name: Saving Program 5733D10 option 11
      ibmi_save_product_to_savf:
        product: 5733D10
        option: 11
        savf_name: MYFILE
        savf_library: MYLIB



Return Values
-------------

  stderr_lines (When rc as non-zero(failure), list, ['CPF9801: Object QNOTE in library L10010125P not found'])
    The standard error split in lines


  job_log (always, str, [{'TO_MODULE': 'QSQSRVR', 'TO_PROGRAM': 'QSQSRVR', 'MESSAGE_TEXT': 'Printer device PRT01 not found.', 'FROM_MODULE': '', 'FROM_PROGRAM': 'QWTCHGJB', 'MESSAGE_TIMESTAMP': '2020-05-20-21.41.40.845897', 'FROM_USER': 'CHANGLE', 'TO_INSTRUCTION': '9369', 'MESSAGE_SECOND_LEVEL_TEXT': 'Cause . . . . . :   This message is used by application programs as a general escape message.', 'MESSAGE_TYPE': 'DIAGNOSTIC', 'MESSAGE_ID': 'CPD0912', 'MESSAGE_LIBRARY': 'QSYS', 'FROM_LIBRARY': 'QSYS', 'SEVERITY': '20', 'FROM_PROCEDURE': '', 'TO_LIBRARY': 'QSYS', 'FROM_INSTRUCTION': '318F', 'MESSAGE_SUBTYPE': '', 'ORDINAL_POSITION': '5', 'MESSAGE_FILE': 'QCPFMSG', 'TO_PROCEDURE': 'QSQSRVR'}])
    the job_log


  stderr (When rc as non-zero(failure), str, CPF9801: Object QNOTE in library L10010125P not found)
    The standard error


  stdout (When rc as 0(success), str, +++ success SAVLICPGM LICPGM(5733D10) DEV(*SAVF) OPTION(*BASE) RSTOBJ(*ALL))
    The standard output


  stdout_lines (When rc as 0(success), list, ['+++ success SAVLICPGM LICPGM(5733D10) DEV(*SAVF) OPTION(*BASE) RSTOBJ(*ALL)'])
    The standard output split in lines


  rc (always, int, 255)
    The task return code (0 means success, non-zero means failure)





Status
------




- This module is not guaranteed to have a backwards compatible interface. *[preview]*


- This module is maintained by community.



Authors
~~~~~~~

- Chang Le (@changlexc)
